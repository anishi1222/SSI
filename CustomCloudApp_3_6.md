# クラウド・アプリケーション定義の完成

完全なクラウド・アプリケーション定義には、トリガー、アクション、スキーマ、およびフローが含まれます。この演習を始めるにあたって部便利なように、以下のコードを使ってクラウド・アプリケーション定義の完成版を作成できます。

1. ダッシュボードでクラウド・アプリケーション定義のタブをクリックする。
2. 編集したいクラウド・アプリケーション定義の下書きをクリックする。下書きのクラウド・アプリケーション定義がない場合、[基本テンプレートからクラウド・アプリケーション定義の作成](CustomCloudApp_3_1.md)の手順に従って新規定義を作成する。
3. クラウド・アプリケーション定義エディタで、クラウド・アプリケーション定義の全てのコードを削除する。
4. 以下のコードをコピー＆ペーストして、トリガー、アクション、スキーマ、フローをクラウド・アプリケーション定義に追加する。
    ```json
    {
        "description": "HubSpot is a marketing application service that manages contacts and campaigns.",
        "categories": [
            "Email Marketing",
            "Marketing"
        ],
        "baseURL": "https://api.hubapi.com",
        "test": {
            "uri": "flow:testConnection"
        },
        "flows": {
            "createContact": {
                "input": {
                    "$ref": "#/schemas/createContactActionInput"
                },
                "output": {
                    "$ref": "#/schemas/createContactActionOutput"
                },
                "step": [
                    {
                        "invoke": {
                            "method": "POST",
                            "uri": "/contacts/v1/contact/",
                            "input": {
                                "body": {
                                    "properties": [
                                        {
                                            "property": "'email'",
                                            "value": "input.email"
                                        },
                                        {
                                            "property": "'firstname'",
                                            "value": "input.firstName"
                                        },
                                        {
                                            "property": "'lastname'",
                                            "value": "input.lastName"
                                        },
                                        {
                                            "property": "'website'",
                                            "value": "input.website"
                                        },
                                        {
                                            "property": "'company'",
                                            "value": "input.company"
                                        },
                                        {
                                            "property": "'phone'",
                                            "value": "input.phone"
                                        },
                                        {
                                            "property": "'address'",
                                            "value": "input.address"
                                        },
                                        {
                                            "property": "'city'",
                                            "value": "input.city"
                                        },
                                        {
                                            "property": "'state'",
                                            "value": "input.state"
                                        },
                                        {
                                            "property": "'zip'",
                                            "value": "input.zip"
                                        }
                                    ]
                                }
                            },
                            "output": "response"
                        }
                    },
                    {
                        "assign": {
                            "from": {
                                "canonical-vid": "response.body['canonical-vid']",
                                "profile-url": "response.body['profile-url']"
                            },
                            "to": "output"
                        }
                    }
                ]
            },
            "testConnection": {
                "step": [
                    {
                        "invoke": {
                            "method": "GET",
                            "uri": "/contacts/v1/lists/all/contacts/all/?count=1",
                            "output": "output",
                            "catchAll": {
                                "throw": {
                                    "errorName": "RuntimeError",
                                    "input": "error.body.error_summary"
                                }
                            }
                        }
                    },
                    {
                        "if": {
                            "condition": "Boolean(!!output.body.contacts)!=true",
                            "then": {
                                "throw": {
                                    "errorName": "RuntimeError"
                                }
                            }
                        }
                    }
                ]
            },
            "onContactCreated_before": {
                "output": {},
                "step": [
                    {
                        "invoke": {
                            "method": "GET",
                            "uri": "/contacts/v1/lists/all/contacts/recent",
                            "input": {
                                "parameters": {
                                    "count": "1"
                                }
                            },
                            "output": "response"
                        }
                    },
                    {
                        "assign": {
                            "from": {
                                "latestCreatedTime": "response.body.contacts[0].addedAt"
                            },
                            "to": "output"
                        }
                    }
                ]
            },
            "onContactCreated_poll": {
                "input": {},
                "output": {
                    "type": "object",
                    "properties": {
                        "persist": {},
                        "notification": {
                            "type": "array",
                            "items": {
                                "type": "object",
                                "properties": {
                                    "vid": {
                                        "type": "integer",
                                        "title": "Contact Id",
                                        "description": "Contact id."
                                    },
                                    "createdate": {
                                        "type": "integer",
                                        "title": "Contact Created Time",
                                        "description": "Contact created time"
                                    },
                                    "firstName": {
                                        "title": "First Name",
                                        "description": "First name",
                                        "type": "string"
                                    },
                                    "lastName": {
                                        "title": "Last Name",
                                        "description": "Last name",
                                        "type": "string"
                                    },
                                    "company": {
                                        "title": "Company",
                                        "description": "Company",
                                        "type": "string"
                                    },
                                    "email": {
                                        "title": "Email",
                                        "description": "Email",
                                        "type": "string"
                                    },
                                    "phone": {
                                        "title": "Phone",
                                        "description": "Phone",
                                        "type": "string"
                                    }
                                }
                            }
                        }
                    }
                },
                "step": [
                    {
                        "invoke": {
                            "method": "GET",
                            "uri": "/contacts/v1/lists/all/contacts/all",
                            "input": {
                                "parameters": {
                                    "count": "100"
                                }
                            },
                            "output": "response"
                        }
                    },
                    {
                        "assign": {
                            "from": "response.body.contacts.map((e)=>{return {vid: e.vid} })",
                            "to": "vidArray"
                        }
                    },
                    {
                        "assign": {
                            "from": [],
                            "to": "contactArray"
                        }
                    },
                    {
                        "while": {
                            "condition": "!isEmpty(vidArray) && index < vidArray.length",
                            "do": [
                                {
                                    "invoke": {
                                        "method": "GET",
                                        "uri": "/contacts/v1/contact/vid/{vid}/profile",
                                        "input": {
                                            "parameters": {
                                                "vid": "vidArray[index].vid"
                                            }
                                        },
                                        "output": "contactResponse"
                                    }
                                },
                                {
                                    "assign": {
                                        "from": "contactArray.concat(contactResponse.body)",
                                        "to": "contactArray"
                                    }
                                }
                            ]
                        }
                    },
                    {
                        "assign": {
                            "from": "contactArray.filter((contact)=>{ return contact.properties.createdate.value.toNumber() > input.latestCreatedTime}).map((e)=>{ return {vid: e.vid, createdate: e.properties.createdate.value.toNumber(), firstName: e.properties.firstname.value,lastName: e.properties.lastname.value,company:e.properties.company.value,email: e.properties.email.value,phone: e.properties.phone.value }})",
                            "to": "newAddedContacts"
                        }
                    },
                    {
                        "if": {
                            "condition": "newAddedContacts.length > 0",
                            "then": {
                                "assign": {
                                    "from": {
                                        "persist": {
                                            "latestCreatedTime": "maxValueBy(newAddedContacts, 'createdate', now().toDate().toMilliseconds())"
                                        },
                                        "notification": "newAddedContacts"
                                    },
                                    "to": "output"
                                }
                            },
                            "else": {
                                "assign": {
                                    "from": {
                                        "persist": {
                                            "latestCreatedTime": "input.latestCreatedTime"
                                        }
                                    },
                                    "to": "output"
                                }
                            }
                        }
                    }
                ]
            },
            "onContactCreated_callback": {
                "input": {
                    "type": "object",
                    "title": "Contact Created",
                    "description": "Contact created",
                    "properties": {
                        "vid": {
                            "type": "integer",
                            "title": "Contact Id",
                            "description": "Contact id."
                        },
                        "createdate": {
                            "type": "integer",
                            "title": "Contact Created Time",
                            "description": "Contact created time"
                        },
                        "firstName": {
                            "title": "First Name",
                            "description": "First name",
                            "type": "string"
                        },
                        "lastName": {
                            "title": "Last Name",
                            "description": "Last name",
                            "type": "string"
                        },
                        "company": {
                            "title": "Company",
                            "description": "Company",
                            "type": "string"
                        },
                        "email": {
                            "title": "Email",
                            "description": "Email",
                            "type": "string"
                        },
                        "phone": {
                            "title": "Phone",
                            "description": "Phone",
                            "type": "string"
                        }
                    }
                },
                "output": {
                    "$ref": "#/schemas/ContactTriggerOutput"
                },
                "step": {
                    "assign": {
                        "from": {
                            "firstName": "input.firstName",
                            "lastName": "input.lastName",
                            "company": "input.company",
                            "createdate": "input.createdate.toDate()",
                            "email": "input.email",
                            "phone": "input.phone"
                        },
                        "to": "output"
                    }
                }
            }
        },
        "schemas": {
            "createContactActionInput": {
                "type": "object",
                "title": "Input",
                "description": "Input",
                "properties": {
                    "email": {
                        "type": "string",
                        "title": "Email",
                        "description": "Email"
                    },
                    "firstName": {
                        "type": "string",
                        "title": "First Name",
                        "description": "First Name"
                    },
                    "lastName": {
                        "type": "string",
                        "title": "Last Name",
                        "description": "Last Name"
                    },
                    "website": {
                        "type": "string",
                        "title": "Website",
                        "description": "Website"
                    },
                    "company": {
                        "type": "string",
                        "title": "Company",
                        "description": "Company"
                    },
                    "address": {
                        "type": "string",
                        "title": "Address",
                        "description": "Address"
                    },
                    "city": {
                        "type": "string",
                        "title": "City",
                        "description": "City"
                    },
                    "state": {
                        "type": "string",
                        "title": "State",
                        "description": "State"
                    },
                    "zip": {
                        "type": "string",
                        "title": "Zip Code",
                        "description": "Zip Code"
                    }
                },
                "required": [
                    "email",
                    "firstName",
                    "lastName"
                ],
                "example": {
                    "email": "ossa.oracle@oracle.com",
                    "firstName": "Oracle",
                    "lastName": "User"
                }
            },
            "createContactActionOutput": {
                "type": "object",
                "title": "Contact",
                "description": "Output",
                "properties": {
                    "canonical-vid": {
                        "type": "integer",
                        "title": "Canonical ID",
                        "description": "Canonical ID"
                    },
                    "profile-url": {
                        "type": "string",
                        "title": "Profile URL",
                        "description": "Profile URL"
                    }
                }
            },
            "ContactTriggerOutput": {
                "title": "Contact",
                "description": "Contact",
                "type": "object",
                "properties": {
                    "firstName": {
                        "title": "First Name",
                        "description": "First name",
                        "type": "string"
                    },
                    "lastName": {
                        "title": "Last Name",
                        "description": "Last name",
                        "type": "string"
                    },
                    "company": {
                        "title": "Company",
                        "description": "Company",
                        "type": "string"
                    },
                    "createddate": {
                        "title": "Contact Created Time",
                        "description": "Contact created time.",
                        "type": "string",
                        "format": "date-time"
                    },
                    "email": {
                        "title": "Email",
                        "description": "Email",
                        "type": "string",
                        "format": "email"
                    },
                    "phone": {
                        "title": "Phone",
                        "description": "Phone",
                        "type": "string"
                    }
                }
            }
        },
        "actions": {
            "createContact": {
                "summary": "Create Contact",
                "description": "This action creates a contact.",
                "input": {
                    "$ref": "#/schemas/createContactActionInput"
                },
                "output": {
                    "$ref": "#/schemas/createContactActionOutput"
                },
                "uri": "flow:createContact"
            }
        },
        "triggers": {
            "onContactCreated": {
                "summary": "Contact Created",
                "description": "This trigger detects when a new contact has been created.",
                "output": {
                    "$ref": "#/schemas/ContactTriggerOutput"
                },
                "type": "poller",
                "split": true,
                "before": {
                    "uri": "flow:onContactCreated_before"
                },
                "poll": {
                    "uri": "flow:onContactCreated_poll"
                },
                "callback": {
                    "uri": "flow:onContactCreated_callback"
                }
            }
        }
    }
    ```
    クラウド・アプリケーション定義のコードを検証し、エラーがでないことを確認する。警告 (warning) が出ることがあるが、これはこのコード例で想定済みのことである
    検証メッセージを理解するには、[OCDL Lint Checks V2](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/app-definition-lint-check.html)を参照。
5. クラウド・アプリケーション定義を保存する。

以後では、クラウド・アプリケーション・インスタンスを作成します。[Creating a Cloud App Instance Using Basic Authentication](https://docs.oracle.com/en/cloud/paas/self-service-integration-cloud/ssiag/creating-cloud-app-instance-using-basic-authentication-type.html)をご覧ください。
