# API Documentation for Work Partner

## Overview

This documentation is intended for the Work Partners of SkillsTrainer who wish to consume SkillsTrainer's APIs and data for their internal purposes. Henceforth, the respective Work Partner will be referred to as the **Client**, the users associated to the Work Partner as **User** and SkillsTrainer as **ST**.

## Prerequisites

The client can access ST APIs with the URL ***https://webapp.skillsscale.in/api/endpoint***

The client will be given a set of auth credentials i.e. an **access key** and a **secret key**. Any request sent from the client to any ST API should have these credentials present in the headers under the keys:

**ST-ACCESS-KEY** = _&lt;access key&gt;_

**ST-SECRET-KEY** = _&lt;secret key&gt;_

## Basic Data flow

- For User

  - Signup

    - User sends Client API signup data
    - Client API sends the signup data to ST API and receives basic profile data and auth tokens
    - Client sends data back to the User

  - Login

    - User sends Client API login data
    - Client API sends the login data to ST API and receives basic profile data and auth tokens
    - Client sends data back to the User

  - Token validation

    - User sends tokens to the Client API
    - Client API sends the tokens for validation to ST API and receives basic profile data and auth tokens
    - Client sends data back to the User

  - Data fetching

    - User inserts the tokens in the request headers to access ST GraphQL

- For Client

  - Login

    - Client API sends the login data to ST API and receives auth tokens

  - Data fetching and API consumption

    - Client inserts the tokens in the request headers to access ST APIs and ST GraphQL

## APIs

### User signup

- Endpoint: **/signup**
- Method: **POST**
- Payload

  - ```
    {
      "full_name": "<FULL NAME>",
      "id": "<EMAIL OR PHONE NUMBER>",
      "password": "<PASSWORD>",
      "source": "<YOUR_COMPANY_NAME>"
    }
    ```

- Response

  - ```
    {
        "access_token": "36a2453a-2ae8-3a74-90e6-af7327325f00",
        "db_user": {
            "email": "abhishek52@gmail.com",
            "id": 582775,
            "idp_user_id": "bd1095da-64cb-4eb8-9d97-cc93695b62af",
            "is_email_verified": false,
            "is_mobile_number_verified": true,
            "mobile_number": "234234222",
            "name": "Abhishek 52",
            "partner_id": null,
            "source": "web"
        },
        "jwt_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUxMiJ9.eyJzdWIiOiJiZDEwOTVkYS02NGNiLTRlYjgtOWQ5Ny1jYzkzNjk1YjYyYWYiLCJpYXQiOjE2NjczMDU4MjYsImV4cCI6MTY2NzMxMzAyNiwiaHR0cHM6Ly9oYXN1cmEuaW8vand0L2NsYWltcyI6eyJ4LWhhc3VyYS1hbGxvd2VkLXJvbGVzIjpbInVzZXIiLCJhZG1pbmlzdHJhdG9yIl0sIngtaGFzdXJhLWRlZmF1bHQtcm9sZSI6InVzZXIiLCJ4LWhhc3VyYS11c2VyLWlkIjoiNTgyNzc1IiwieC1oYXN1cmEtcm9sZSI6InVzZXIifX0.LsHRug2Kgy3uWjbYnRyXJvMZ-UZDnTBRFIKhyl57Oyq3nEGHiixRPtFH7l7AE1KV1UW1OWIeeRpse27Abl31CBcYf_r28rTEKAjpqH_J12w5--YIZTZTV-VjXMNa_6WTN6MuY-Yc13jTrtCWiBmKlkIoPbPgFrYC2VhR9wxzloPbY5XlOx4xyfNRD3FSBAxlSOudE3WcOMv1_xktplTHB2rlE64qsG7nhRZstBJ5tMhwuWIT0ktH2SAdu_fOgBeTeHuK4nX8cmxsBYEVZ_wm9GvLWcdsM5BV0a4pZUWoUzewxcgc1heVEqUdOUOrVyOUOZfRLUnSAyaH_EjXT6M0ZA",
        "success": true
    }
    ```

### User login

- Endpoint: **/login**
- Method: **POST**
- Payload

  - ```
    {
        "id": "<EMAIL OR PHONE NUMBER>",
        "password": "<PASSWORD>"
    }
    ```

- Response

  - ```
      {
        "access_token": "388c8ac6-bf8d-30d0-941e-482bd17d6d75",
        "db_user": {
            "email": "abhishek20@gmail.com",
            "id": 21,
            "idp_user_id": "7dc8a5f6-e213-4719-9a06-53bdad73154e",
            "is_email_verified": false,
            "is_mobile_number_verified": false,
            "mobile_number": "2342342223",
            "name": "Abhishek 20",
            "partner_id": null,
            "source": "web"
        },
        "jwt_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUxMiJ9.eyJzdWIiOiI3ZGM4YTVmNi1lMjEzLTQ3MTktOWEwNi01M2JkYWQ3MzE1NGUiLCJpYXQiOjE2Njc0MDAwNzMsImV4cCI6MTY2NzQwNzI3MywiaHR0cHM6Ly9oYXN1cmEuaW8vand0L2NsYWltcyI6eyJ4LWhhc3VyYS1hbGxvd2VkLXJvbGVzIjpbInVzZXIiLCJhZG1pbmlzdHJhdG9yIl0sIngtaGFzdXJhLWRlZmF1bHQtcm9sZSI6InVzZXIiLCJ4LWhhc3VyYS11c2VyLWlkIjoiMjEiLCJ4LWhhc3VyYS1yb2xlIjoidXNlciJ9fQ.eL1V8Idy_NzoffmEa5fkKx9lYjrt8KFE-OmJbDCHNinQFG2UO8BlPuOPRZ2B1IyErLQ8xLpfGDfs8h815_Hx0y7mtJ5yWIvak-5RkZ7tg5tw9lcM0bbTlr_2TwCbr1gbF3U1FY9jmABgcKygHnd46yeR9hj6m-yqqXiZIn00vheY6Yh50Xhl0A1Z11f__rlW6QYf1hQwuTS22VcllA6kLeAVs1Tse2RAFTR0e_adphnV-M0-HhmuwpSimIuhqAHxMsqet4CyN1eneMM3kBkbhJvSG3_cGNHhUz9_8pEKYLQpYDW1FZEBR6l7zEu8ZYOMTuhpO-9lAdT4fa_WWdrJwQ",
        "success": true,
        "user": {
            "emails": [
                "abhishek20@gmail.com"
            ],
            "id": "7dc8a5f6-e213-4719-9a06-53bdad73154e",
            "meta": {
                "created": "2021-12-06T12:05:10.562533Z",
                "lastModified": "2021-12-06T12:05:10.562533Z",
                "location": "https://localhost:9443/scim2/Users/7dc8a5f6-e213-4719-9a06-53bdad73154e",
                "resourceType": "User"
            },
            "name": {
                "familyName": "Abhishek 20",
                "givenName": "Abhishek"
            },
            "phoneNumbers": [
                {
                    "type": "mobile",
                    "value": "234234222"
                }
            ],
            "roles": [
                {
                    "display": "everyone"
                }
            ],
            "userName": "SKILLSTRAINER/abhishek20-1638792310"
        }
    }
    ```

### User token validation

- Endpoint: **/validate_cookie**
- Method: **POST**
- Headers

  - **jwt_token**: &lt;jwt_token&gt;
  - **access_token**: &lt;access_token&gt;

- Payload: _None_
- Response:

  - ```
    {
        "data": {
            "access_token": "f8275d99-d054-3a41-a442-6d2cdfcea5c4",
            "db_user": {
                "email": "abhishek20@gmail.com",
                "id": 21,
                "idp_user_id": "7dc8a5f6-e213-4719-9a06-53bdad73154e",
                "is_email_verified": false,
                "is_mobile_number_verified": false,
                "mobile_number": "2342342223",
                "name": "Abhishek 20",
                "partner_id": null,
                "source": "web"
            },
            "jwt_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUxMiJ9.eyJzdWIiOiI3ZGM4YTVmNi1lMjEzLTQ3MTktOWEwNi01M2JkYWQ3MzE1NGUiLCJpYXQiOjE2Njc4MDMwMDEsImV4cCI6MTY2NzgxMDIwMSwiaHR0cHM6Ly9oYXN1cmEuaW8vand0L2NsYWltcyI6eyJ4LWhhc3VyYS1hbGxvd2VkLXJvbGVzIjpbInVzZXIiLCJhZG1pbmlzdHJhdG9yIl0sIngtaGFzdXJhLWRlZmF1bHQtcm9sZSI6InVzZXIiLCJ4LWhhc3VyYS11c2VyLWlkIjoiMjEiLCJ4LWhhc3VyYS1yb2xlIjoidXNlciJ9fQ.i6neu-pLPuv5o7cdeCnYBk3i5QErO16lOXQa0Ol_FqOq77RfJOKN4YAzKNyxtl9fWioqYEaTVzv_UgefyAc6lJHun-cY3-jdbFFPkXzDWOxkciEexj7gfcjt9NmCsaEmDTV6-zIhFcOs6KW4fJx-bap7Hwxws7kRzoUb3xFuMLDfxPXYbBu6svyPblT5JH2TUpN1bEMaK2_b2OXvyIwzdosnpbfaJEzLFS-JcGeADKAlJWr7HcXSXRQyAPgD6JaDiLZePLitvB6p4E6rVwKWV5XL2ZD5nRlWXOSgahxIfGxU2zWoh-zoAPjA-twP1xyvSWK3alslzDmU2ke6T8wwfA",
            "success": true,
            "user": {
                "emails": [
                    "abhishek20@gmail.com"
                ],
                "id": "7dc8a5f6-e213-4719-9a06-53bdad73154e",
                "meta": {
                    "created": "2021-12-06T12:05:10.562533Z",
                    "lastModified": "2021-12-06T12:05:10.562533Z",
                    "location": "https://localhost:9443/scim2/Users/7dc8a5f6-e213-4719-9a06-53bdad73154e",
                    "resourceType": "User"
                },
                "name": {
                    "familyName": "Abhishek 20",
                    "givenName": "Abhishek"
                },
                "phoneNumbers": [
                    {
                        "type": "mobile",
                        "value": "234234222"
                    }
                ],
                "roles": [
                    {
                        "display": "everyone"
                    }
                ],
                "userName": "SKILLSTRAINER/abhishek20-1638792310"
            }
        },
        "success": true
    }
    ```

### Enrol user in a paid course

Enrolling a user in a paid course requires a coupon code which will be provided by SkillsTrainer.

- Endpoint: **/apply_coupon**
- Method: **POST**
- Headers
  - **jwt_token**: &lt;jwt_token&gt;
  - **access_token**: &lt;access_token&gt;
- Payload:
  - ```
    {
      "coupon_code": "<COUPON_CODE>",
    }
    ```
- Response: The returned ID is the coupon application ID
  - ```
    {
      "success": True,
      "data": {
        "id": 33453
      }
    }
    ```

### Get a user's course data

- Endpoint: /get_moodle_courses_for_user
- Method: POST
- Payload:
  - ```
    {
      "user_id": 28
    }
    ```
- Response: Moodle data for the courses is returned
  - ```
    {
      "data": [
        {
          "category": 1,
          "completed": false,
          "completionhascriteria": true,
          "completionusertracked": true,
          "displayname": "Work Readiness",
          "enablecompletion": true,
          "enddate": 2038501800,
          "enrolledusercount": 20933,
          "format": "topics",
          "fullname": "Work Readiness",
          "hidden": false,
          "id": 58,
          "idnumber": "118047320200623082120",
          "isfavourite": false,
          "lang": "",
          "lastaccess": 1663394223,
          "marker": 0,
          "overviewfiles": [
            {
              "filename": "JOB Readiness.png",
              "filepath": "/",
              "filesize": 254731,
              "fileurl": "https://lms.skillstrainer.in/moodle/webservice/pluginfile.php/23901/course/overviewfiles/JOB%20Readiness.png",
              "mimetype": "image/png",
              "timemodified": 1590081005
            }
          ],
          "progress": 47.05882352941176,
          "shortname": "Work Readiness Course",
          "showgrades": true,
          "startdate": 1564425000,
          "summary": "",
          "summaryformat": 1,
          "visible": 1
        },
        {
          "category": 1,
          "completed": false,
          "completionhascriteria": true,
          "completionusertracked": true,
          "displayname": "वर्क  रेडीनेस - हिंदी ",
          "enablecompletion": true,
          "enddate": 1693954800,
          "enrolledusercount": 1186,
          "format": "topics",
          "fullname": "वर्क  रेडीनेस - हिंदी ",
          "hidden": false,
          "id": 60,
          "idnumber": "1450",
          "isfavourite": false,
          "lang": "",
          "lastaccess": 1660022562,
          "marker": 0,
          "overviewfiles": [
            {
              "filename": "JOB Readiness.png",
              "filepath": "/",
              "filesize": 254731,
              "fileurl": "https://lms.skillstrainer.in/moodle/webservice/pluginfile.php/25031/course/overviewfiles/JOB%20Readiness.png",
              "mimetype": "image/png",
              "timemodified": 1590081036
            }
          ],
          "progress": 6.25,
          "shortname": "WRP_Hindi",
          "showgrades": true,
          "startdate": 1567810800,
          "summary": "",
          "summaryformat": 1,
          "visible": 1
        },
        {
          "category": 11,
          "completed": false,
          "completionhascriteria": false,
          "completionusertracked": true,
          "displayname": "Retail Sales Associate (Sign Language)",
          "enablecompletion": true,
          "enddate": 0,
          "enrolledusercount": 4,
          "format": "topics",
          "fullname": "Retail Sales Associate (Sign Language)",
          "hidden": false,
          "id": 164,
          "idnumber": "",
          "isfavourite": false,
          "lang": "",
          "lastaccess": 1660888412,
          "marker": 0,
          "overviewfiles": [
            {
              "filename": "RTA New.png",
              "filepath": "/",
              "filesize": 960969,
              "fileurl": "https://lms.skillstrainer.in/moodle/webservice/pluginfile.php/1595639/course/overviewfiles/RTA%20New.png",
              "mimetype": "image/png",
              "timemodified": 1659245523
            }
          ],
          "progress": 0,
          "shortname": "Retail Sales Associate (Sign Language)",
          "showgrades": true,
          "startdate": 1659292200,
          "summary": "",
          "summaryformat": 1,
          "visible": 1
        }
      ]
    }
    ```

### Get a user's certificate

- Endpoint: /complete_course
- Method: POST
- Payload:
  - ```
    {
      "access_secret": <YOUR-ACCESS-SECRET>,
      "user_id": 590254,
      "course_id": 50,
      "force_complete": true,
    }
    ```
- Response:
  - ```
    {
      "success": true,
      "download_link": "https://adminskillstrainerprod.s3.ap-south-1.amazonaws.com/certificates/1676631049493"
    }
    ```

### Delete users

- Endpoint: /delete_users
- Method: POST
- Payload:
  - ```
    {
      access_secret: "<PROVIDED_ACCESS_SECRET>",
      "user_ids": [28, 29, 31] // List of user IDs
    }
    ```
- Repsonse:

  - ```
    {
      "data": {
        "hasura_deletion_response": {
          "delete_courses_batch_trainee_attendences": {
            "affected_rows": 0
          },
          "delete_courses_bulk_certificates_details": {
            "affected_rows": 0
          },
          "delete_courses_certificates": {
            "affected_rows": 0
          },
          "delete_courses_course_criteria_users": {
            "affected_rows": 0
          },
          "delete_courses_course_module_completion": {
            "affected_rows": 0
          },
          "delete_courses_course_module_user_attempt": {
            "affected_rows": 0
          },
          "delete_courses_course_scorm_track_data": {
            "affected_rows": 0
          },
          "delete_courses_partner_project_users": {
            "affected_rows": 0
          },
          "delete_courses_partner_users": {
            "affected_rows": 0
          },
          "delete_courses_scholarship_partner_user": {
            "affected_rows": 0
          },
          "delete_courses_social_metadata": {
            "affected_rows": 1
          },
          "delete_courses_st_user_coupons": {
            "affected_rows": 0
          },
          "delete_courses_user_academic_qualifications": {
            "affected_rows": 0
          },
          "delete_courses_user_address": {
            "affected_rows": 0
          },
          "delete_courses_user_batch_enrollment": {
            "affected_rows": 0
          },
          "delete_courses_user_batch_slots": {
            "affected_rows": 0
          },
          "delete_courses_user_course_complete": {
            "affected_rows": 0
          },
          "delete_courses_user_course_enrolment": {
            "affected_rows": 0
          },
          "delete_courses_user_course_order": {
            "affected_rows": 0
          },
          "delete_courses_user_course_question_attemept": {
            "affected_rows": 0
          },
          "delete_courses_user_course_quiz_attempt": {
            "affected_rows": 0
          },
          "delete_courses_user_course_subscription": {
            "affected_rows": 0
          },
          "delete_courses_user_family_details": {
            "affected_rows": 0
          },
          "delete_courses_user_identity_documents": {
            "affected_rows": 0
          },
          "delete_courses_user_tags": {
            "affected_rows": 0
          },
          "delete_courses_user_work_details": {
            "affected_rows": 0
          },
          "delete_courses_users": {
            "affected_rows": 1
          }
        },
        "moodle_deletion_response": [
          {
            "response": null,
            "user_id": 589362
          }
        ],
        "wso2_deletion_response": [
          {
            "response": "",
            "user_id": 589362
          }
        ]
      },
      "success": true
    }
    ```

### Get user registration details

- Endpoint: /get_user_details
- Method: POST
- Payload:
  - ```
    {
      access_secret: "<PROVIDED_ACCESS_SECRET>",
      "user_emails": ["abhishek.challa.97@gmail.com"]
    }
    ```
- Repsonse:
  ```
  {
    "data": [
      {
        "db_user": {
          "email": "abhishek.challa.97@gmail.com",
          "id": 589402,
          "idp_user_id": "db580888-ef35-4110-bafc-ecc81bd869e6",
          "idp_user_name": "SKILLSTRAINER/abhishekchalla-1680069614",
          "source": "web"
        },
        "email": "abhishek.challa.97@gmail.com",
        "idp_user": {
          "emails": [
            "abhishek.challa.97@gmail.com"
          ],
          "id": "db580888-ef35-4110-bafc-ecc81bd869e6",
          "is_associated_to_db_user": true,
          "meta": {
            "created": "2023-03-29T06:00:15.264787Z",
            "lastModified": "2023-03-29T06:00:15.264787Z",
            "location": "https://localhost:9443/scim2/Users/db580888-ef35-4110-bafc-ecc81bd869e6",
            "resourceType": "User"
          },
          "name": {
            "familyName": "Abhishek Challa",
            "givenName": "Abhishek"
          },
          "phoneNumbers": [
            {
              "type": "mobile",
              "value": "234234222"
            }
          ],
          "roles": [
            {
              "display": "everyone"
            }
          ],
          "userName": "SKILLSTRAINER/abhishekchalla-1680069614"
        },
        "moodle_user": {
          "auth": "manual",
          "confirmed": true,
          "department": "",
          "email": "abhishek.challa.97@gmail.com",
          "firstaccess": 0,
          "firstname": "Abhishek",
          "fullname": "Abhishek Abhishek",
          "id": 859172,
          "is_associated_to_db_user": true,
          "lang": "en",
          "lastaccess": 0,
          "lastname": "Abhishek",
          "mailformat": 1,
          "profileimageurl": "https://lms.skillstrainer.in/moodle/theme/image.php/adaptable/core/1678347801/u/f1",
          "profileimageurlsmall": "https://lms.skillstrainer.in/moodle/theme/image.php/adaptable/core/1678347801/u/f2",
          "suspended": false,
          "theme": "",
          "timezone": "99",
          "username": "abhishekchalla-1680069614"
        }
      }
    ],
    "success": true
  }
  ```

## Data Fetching

Data can be fetched directly from ST's Hasura GraphQL Engine. Data is fetched using **queries** and created, updated or deleted using **mutations** (For more information on GraphQL usage, visit [https://hasura.io/docs/latest/index/](https://hasura.io/docs/latest/index/)).

The Client needs to make the following network call to execute queries / mutations and CRUD the required data and will receive the execution result in JSON as the response.

Endpoint: [https://graphql.skillstrainer.in/v1/graphql](https://graphql.skillstrainer.in/v1/graphql)

Method: **POST**

Payload:

- ```
  {
    "query": "<QUERY/MUTATION TO CRUD THE REQUIRED DATA>",
    "variables": "<VARIABLES REQUIRED BY THE QUERY/MUTATION>"
  }
  ```

The Client can use the following queries / mutations to make frequently required CRUD operations

### Queries

- Fetch Course data

  - ```
    query ($courseId: bigint) {
      courses_course(where: {id: {_eq: $courseId}}) {
        id
        full_name
        description
        start_date
        end_date
        moodle_config_id
        moodle_course_url
        course_category {
          id
          name
        }
        publish
        is_moodle_course
        created_at
        updated_at
        identifier
        cost
        nsqf_level
        discount
        multilang
        image_url
        short_name
        moodle_course_id
        duration
        is_live_course
        is_subscription
        is_taxable
        course_type
      }
    }

    ```

- Fetch User data

  - ```
    query ($userId: bigint) {
      courses_users (where: { id: { _eq: $userId } }) {
        name
        partner_id
        instructor_id
        mobile_number
        email
        activation_start_date
        activation_end_date
        active
        id
        created_at
        updated_at
        idp_user_id
        source
        gender
        date_of_birth
        social_category
        address_complete
        address_id
        facebook_user_id
        google_user_id
        idp_user_name
        is_email_verified
        is_mobile_number_verified
        enrollments {
          id
          course_id
          user_id
          enroll_status
          created_at
          updated_at
          exired_at
          order_id
          subscription_id
          partner_id
          course: course_obj_relation {
            id
            full_name
            description
            start_date
            end_date
            moodle_config_id
            moodle_course_url
            course_category {
              id
              name
            }
            publish
            is_moodle_course
            created_at
            updated_at
            identifier
            cost
            nsqf_level
            discount
            multilang
            image_url
            short_name
            moodle_course_id
            duration
            is_live_course
            is_subscription
            is_taxable
            course_type
          }
        }
        user_academic_qualifications {
          qualification_type
          institution_name
          qualification_name
          marks
          institution_address_id
          contact_person_name
          contact_person_type
          contact_person_email
          contact_person_mobile_number
          user_id
          achievement
          document_proof_id
          document_proof_url
          id
          updated_at
          created_at
          marking_type
          document_proof: user_identity_document {
            document_type
            name
            url
            user_id
            id
            created_at
            updated_at
            description
          }
          address: user_address {
            adress_type
            id
            created_at
            updated_at
            city_town
            pincode
            district
            state
            country
            location
            house_number
            country_iso_code
            user_id
          }
        }
        user_family_details {
          member_type
          occupation
          mobile_number
          email
          is_currently_working
          income_certficate_document_id
          income_certificate_url
          user_id
          id
          created_at
          updated_at
          name
          annual_income
          income_certficate {
            document_type
            name
            url
            user_id
            id
            created_at
            updated_at
            description
          }
        }
        user_languages {
          user_id
          language_id
          can_speak
          can_read
          can_write
          created_at
          updated_at
          id
          language: st_language {
            id
            name
          }
        }
        user_skills {
          user_id
          st_skill_id
          st_skill_name
          document_proof_url
          created_at
          updated_at
          id
        }
        user_work_details {
          title
          company_name
          start_date
          end_date
          place
          user_id
          created_at
          updated_at
          id
        }
      }
    }
    ```

- Fetch User course progress

  - ```
    query getUserCourseProgress(
      $course_id: Int, $user_id: Int
    ) {
      courses_course_section(
        where: {
          course_id: {
            _eq: $course_id
          }
        }
      ) {
        id
        name
        subsections: coursesec {
          name
          id
          user_completion_status: course_complete_module_array (where: {
            user_id: { _eq: $user_id }
          }) {
            completion_status
            mapping_id
            completion_date
            user_id
          }
        }
      }
    }
    ```

- Fetch course modules

  - ```
    query getCourseModules ($course_id: Int) {
      courses_course_section (
        where: {
          course_id: { _eq: $course_id }
        }
      ) {
        id
        name
        coursesec {
          id
          name
        }
      }
    }
    ```
