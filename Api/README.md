[Uploa{
	"info": {
		"_postman_id": "91894e8e-c895-4dfa-8c62-6b81bbd55873",
		"name": "Adjutor API Service",
		"description": "Adjutor is the API service from Lendsqr provided via RESTful APIs. The services include the following:\n\n- Authorizing direct debit, with consent, for repayments\n    \n- Getting the bank accounts, with consent, tied to a customer's BVN\n    \n- Matching a customer image against what's on their BVN\n    \n- Getting the name and details of a bank account number\n    \n- Getting credit information about a borrower\n    \n- Getting \"probable\" fraud information from our Karma blacklist\n    \n- Accessing credit performance information, for a borrower, from the Lendsqr ecosystem\n    \n\n## Getting Started\n\nTo have access to our APIs is easy.\n\n1. [Sign up for a Lendsqr Adjutor account](https://app.adjutor.io/signup?source=adjutor-api-documentation)\n    \n2. Then create an app and select the services required fror the app\n    \n\n## Terms of Use\n\nTo use Lendsqr Adjutor APIs, you must agree to our terms of use. These terms outline the conditions under which you may access and use our API. Please review these terms carefully before using our API. If you have any questions or concerns about these terms, please contact us at [api@lendsqr.com](https://mailto:api@lendsqr.com).\n\n[You read about our terms here](https://adjutor.io/legal/terms-of-use).\n\n## Getting Support\n\nIf you require assistance at any time when using this documentation or the services, please email [api@lendsqr.com](https://mailto:api@lendsqr.com) and someone would be in touch with you as soon as possible. If you are currently using Lendsqr to lend, you can also contact your account manager at [growth@lendsqr.com](https://mailto:growth@lendsqr.com).\n\n---\n\n# Authentication\n\nAuthentication to the Adjutor API service is performed with the API key. Every endpoint requires authentication, so you will need to add the following header to each request:\n\n`Authorization: Bearer`\n\n`base_url: https://adjutor.lendsqr.com/v2/`\n\n---\n\n# Data Types\n\nAll of the API responses returned are in JSON format, with these data types defined below:\n\n| Type | Description |\n| --- | --- |\n| `string` | A UTF-8 encoded string |\n| `number` | An integer |\n| `datetime` | An ISO8601 encoded DateTime. All datetimes are returned in UTC with offset +00:00 |\n| `decimal` | All monetary values are returned with up to two decimal places and may be positive (20.78) or negative (-32.50) |\n\n# Data Length\n\n| Type | Description | Length |\n| --- | --- | --- |\n| Text fields | `string` | max-length 255 characters |\n| BVN | `integers` starting with 1 or 2 | 11 digits. |\n| Account Number | `integers` | 10 digits. |\n\n---\n\n# Response\n\n| Field | Type | Description |\n| --- | --- | --- |\n| data | `array` | The actual data items you have requested |\n| meta | `object` | Key/value information that is not essential to understanding the resources returned but offers additional detail |\n\n# Meta\n\n| Field | Type | Description |\n| --- | --- | --- |\n| cost | `number` | The cost for the API call in Naira |\n| balance | `number` | The remaining balance in your service wallet in Naira |\n\n---\n\n# Errors\n\nErrors are expressed as a combination of HTTP status codes and an accompanying JSON body providing required detail where possible. You should be able to rely on the HTTP status code alone to determine the cause of the problem.\n\n## Error Response Fields\n\n| Field | Type |\n| --- | --- |\n| message | `string` A human-readable message as to the specifics of the problem. For example, it may contain a detail description of what caused the problem |\n| status number | The HTTP status code used in the response |\n| error_code | `number` |\n\n---",
		"schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json",
		"_exporter_id": "39541371"
	},
	"item": [
		{
			"name": "Validation",
			"item": [
				{
					"name": "Bank Verification Number",
					"item": [
						{
							"name": "Initialize BVN Consent",
							"request": {
								"method": "POST",
								"header": [
									{
										"key": "Authorization",
										"value": "",
										"type": "text",
										"disabled": true
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"contact\": \"08012345678\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}verification/bvn/:bvn",
									"host": [
										"{{base_url}}verification"
									],
									"path": [
										"bvn",
										":bvn"
									],
									"variable": [
										{
											"key": "bvn",
											"value": "22222222222"
										}
									]
								},
								"description": "This endpoint is used to initiate the process for getting the customer's consent. The integrator is required to pass the customer's BVN and the phone number. If the phone number passed does not match the customer phone on record, an error is returned but with a masked collection of the correct phone and email on the customer account.\n\n#### Request Body\n\n| Field | Type | Description |\n| --- | --- | --- |\n| contact | `String` | The phone number or email of the customer. At the minimum, the phone number must be the one registered to the BVN (e.g., 08012345678, [ado@example.com](https://mailto:ado@example.com)). |"
							},
							"response": [
								{
									"name": "Initialize BVN",
									"originalRequest": {
										"method": "POST",
										"header": [
											{
												"key": "Authorization",
												"value": "",
												"type": "text",
												"disabled": true
											}
										],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"contact\": \"0808***2636\"\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "https://adjutor.lendsqr.com/v2/verification/bvn/:bvn",
											"protocol": "https",
											"host": [
												"adjutor",
												"lendsqr",
												"com"
											],
											"path": [
												"v2",
												"verification",
												"bvn",
												":bvn"
											],
											"variable": [
												{
													"key": "bvn",
													"value": ""
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 21 Feb 2024 07:04:59 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "91cddf27-e8c8-4475-a69f-41d3cfd2c78e"
										},
										{
											"key": "Last-Modified",
											"value": "Wed, 21 Feb 2024 07:04:38 GMT"
										},
										{
											"key": "ETag",
											"value": "W/\"75-9VH2gGmZSDLe6+ZLGrXFVt5sc5Y\""
										},
										{
											"key": "CF-Cache-Status",
											"value": "DYNAMIC"
										},
										{
											"key": "Server",
											"value": "cloudflare"
										},
										{
											"key": "CF-RAY",
											"value": "858d22e9cc0a6622-AMS"
										},
										{
											"key": "Content-Encoding",
											"value": "gzip"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"otp\",\n    \"message\": \"Please provide OTP sent to contact\",\n    \"data\": \"0808***2636\",\n    \"meta\": {\n        \"cost\": 0,\n        \"balance\": 4815\n    }\n}"
								}
							]
						},
						{
							"name": "Complete Consent and get BVN Details",
							"request": {
								"method": "PUT",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"otp\": \"623553\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}verification/bvn/:bvn",
									"host": [
										"{{base_url}}verification"
									],
									"path": [
										"bvn",
										":bvn"
									],
									"variable": [
										{
											"key": "bvn",
											"value": ""
										}
									]
								},
								"description": "This endpoint is used to get the BVN data after the customer's consent has been approved.\n\n### Response fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| reference | `integer` | Unique reference number (e.g., 10000001) |\n| bvn | `string` | Bank Verification Number (e.g., \"22123456789\") |\n| first_name | `string` | First name of the individual (e.g., \"ADO\") |\n| middle_name | `string` | Middle name of the individual (e.g., \"JOHN\") |\n| last_name | `string` | Last name of the individual (e.g., \"SULE\") |\n| dob | `date` | Date of birth in YYYY-MM-DD format (e.g., \"1990-10-31\") |\n| formatted_dob | `date` | Formatted date of birth (e.g., \"1990-10-31\") |\n| mobile2 | `string` | Secondary mobile number, if applicable (e.g., 08012345678) |\n| mobile | `string` | Primary mobile number (e.g., \"08012345678\") |\n| registration_date | `string` | Date of registration (e.g., \"30-Mar-2015\") |\n| enrollment_bank | `string` | Bank enrollment number (e.g., \"044\") |\n| enrollment_branch | `string` | Branch of enrollment (e.g., \"RET SHOP - BABCOCK UNIVERSITY (137)\") |\n| email | `string` | Email address (e.g., \"[wunmi@yahoo.com](https://mailto:wunmi@yahoo.com)\") |\n| gender | `string` | Gender (e.g., \"Male\") |\n| level_of_account | `string` | Level of account, if applicable (e.g., Tier 2) |\n| lga_of_origin | `string` | Local Government Area of origin (e.g., \"Abeokuta South\") |\n| lga_of_residence | `string` | Local Government Area of residence (e.g., \"Abeokuta South\") |\n| marital_status | `string` | Marital status (e.g., \"Single\") |\n| nin | `string` | National Identification Number, if applicable (e.g., 1234567890) |\n| name_on_card | `string` | Name as it appears on card (e.g., \"ADO JOHN SULE\") |\n| nationality | `string` | Nationality, if applicable (e.g., American) |\n| residential_address | `string` | Residential address (e.g., \"Ogun State\") |\n| state_of_origin | `string` | State of origin (e.g., \"Ogun State\") |\n| state_of_residence | `string` | State of residence (e.g., \"Ogun State\") |\n| watchlisted | `integer` | Watchlist status (e.g., 0 for not watchlisted) |\n| image_url | `string` | URL of the photo (e.g., \"[https://picsum.photos/id/1/5000/3333\"](https://picsum.photos/id/1/5000/3333)) |"
							},
							"response": [
								{
									"name": "Complete BVN Verification",
									"originalRequest": {
										"method": "PUT",
										"header": [],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"otp\": \"242366\"\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "https://adjutor.lendsqr.com/v2/verification/bvn/:bvn",
											"protocol": "https",
											"host": [
												"adjutor",
												"lendsqr",
												"com"
											],
											"path": [
												"v2",
												"verification",
												"bvn",
												":bvn"
											],
											"variable": [
												{
													"key": "bvn",
													"value": ""
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 21 Feb 2024 07:05:26 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "e522b3f8-6d99-4a10-88e1-e4b962c1f854"
										},
										{
											"key": "Last-Modified",
											"value": "Wed, 21 Feb 2024 07:05:14 GMT"
										},
										{
											"key": "ETag",
											"value": "W/\"3de-C/X9feDDVRhWa/gVl6sTmdaWpko\""
										},
										{
											"key": "CF-Cache-Status",
											"value": "DYNAMIC"
										},
										{
											"key": "Server",
											"value": "cloudflare"
										},
										{
											"key": "CF-RAY",
											"value": "858d23c7ba346622-AMS"
										},
										{
											"key": "Content-Encoding",
											"value": "gzip"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"Successful\",\n    \"data\": {\n        \"reference\": 10000001,\n        \"bvn\": \"22123456789\",\n        \"first_name\": \"ADO\",\n        \"middle_name\": \"JOHN\",\n        \"last_name\": \"SULE\",\n        \"dob\": \"1990-10-31\",\n        \"formatted_dob\": \"1990-10-31\",\n        \"mobile2\": null,\n        \"mobile\": \"08012345678\",\n        \"registration_date\": \"30-Mar-2015\",\n        \"enrollment_bank\": \"044\",\n        \"enrollment_branch\": \"RET SHOP - BABCOCK UNIVERSITY (137)\",\n        \"email\": \"wunmi@yahoo.com\",\n        \"gender\": \"Male\",\n        \"level_of_account\": null,\n        \"lga_of_origin\": \"Abeokuta South\",\n        \"lga_of_residence\": \"Abeokuta South\",\n        \"marital_status\": \"Single\",\n        \"nin\": null,\n        \"name_on_card\": \"ADO JOHN SULE\",\n        \"nationality\": null,\n        \"residential_address\": \"Ogun State\",\n        \"state_of_origin\": \"Ogun State\",\n        \"state_of_residence\": \"Ogun State\",\n        \"watchlisted\": 0,\n        \"base64Image\": null,\n        \"image_url\": \"https://picsum.photos/id/1/5000/3333\"\n    },\n    \"meta\": {\n        \"cost\": 20,\n        \"balance\": 4815\n    }\n}"
								}
							]
						}
					],
					"description": "Bank Verification Number (BVN) is the national ID system created by Nigerian banks to uniquely identified bank customers in the Nigerian banking ecosystem.\n\nThe banking ecosystem has also created a mechanism where all the bank accounts tied to a specific BVN could be gotten."
				},
				{
					"name": "Get Accounts for a BVN",
					"item": [
						{
							"name": "Initialize BVN Accounts Consent",
							"request": {
								"method": "POST",
								"header": [
									{
										"key": "Authorization",
										"value": "",
										"type": "text",
										"disabled": true
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"contact\": \"08012345678\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}verification/bvn/:bvn/accounts",
									"host": [
										"{{base_url}}verification"
									],
									"path": [
										"bvn",
										":bvn",
										"accounts"
									],
									"variable": [
										{
											"key": "bvn",
											"value": ""
										}
									]
								},
								"description": "This endpoint is used to initiate the process for getting customer consent. The integrator is required to pass the customer's BVN and the phone number.\n\n**If the phone number passed does not match the customer phone on record, an error is returned but with a masked collection of the correct phone and email on the customer account.**\n\n``` json\n{\n  \"status\": \"otp\",\n  \"message\": \"Please provide OTP sent to contact\",\n  \"data\": \"ado****@example.com\",\n  \"meta\": {\n    \"cost\": 0,\n    \"balance\": 4735\n  }\n}\n\n ```\n\n#### Request Body\n\n| Field | Type | Description |\n| --- | --- | --- |\n| contact | `String` | The phone number or email of the customer. At the minimum, the phone number must be the one registered to the BVN (e.g., 08012345678, [ado@example.com](https://mailto:ado@example.com)). |"
							},
							"response": [
								{
									"name": "Initialize BVN Accounts",
									"originalRequest": {
										"method": "POST",
										"header": [
											{
												"key": "Authorization",
												"value": "",
												"type": "text",
												"disabled": true
											}
										],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"contact\": \"ado****@example.com\"\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "https://adjutor.lendsqr.com/v2/verification/bvn/:bvn/accounts",
											"protocol": "https",
											"host": [
												"adjutor",
												"lendsqr",
												"com"
											],
											"path": [
												"v2",
												"verification",
												"bvn",
												":bvn",
												"accounts"
											],
											"variable": [
												{
													"key": "bvn",
													"value": ""
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 21 Feb 2024 07:17:45 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "83e56b5f-fa1e-40d6-a987-79e05cee8fa8"
										},
										{
											"key": "Last-Modified",
											"value": "Wed, 21 Feb 2024 07:17:30 GMT"
										},
										{
											"key": "ETag",
											"value": "W/\"86-slc23G5+RJfJHR9MiSZECE5kUCk\""
										},
										{
											"key": "CF-Cache-Status",
											"value": "DYNAMIC"
										},
										{
											"key": "Server",
											"value": "cloudflare"
										},
										{
											"key": "CF-RAY",
											"value": "858d35bfa8556622-AMS"
										},
										{
											"key": "Content-Encoding",
											"value": "gzip"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"otp\",\n    \"message\": \"Please provide OTP sent to contact\",\n    \"data\": \"ado****@example.com\",\n    \"meta\": {\n        \"cost\": 0,\n        \"balance\": 4735\n    }\n}"
								}
							]
						},
						{
							"name": "Complete Consent and Get BVN Accounts",
							"request": {
								"method": "PUT",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"otp\": \"477226\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}verification/bvn/:bvn/accounts",
									"host": [
										"{{base_url}}verification"
									],
									"path": [
										"bvn",
										":bvn",
										"accounts"
									],
									"variable": [
										{
											"key": "bvn",
											"value": ""
										}
									]
								},
								"description": "This endpoint is used to get the bank accounts. It requires the OTP that has been sent to the customer. OTP to phones are usually sent from PFAlert sender id.\n\n#### Request Body\n\n| Field | Type | Description |\n| --- | --- | --- |\n| otp | `string` | The one-time password for verification (e.g., \"477226\"). |\n\n#### Response Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| account_name | `string` | The name of the account holder (e.g., \"ADO JOHN SULE\"). |\n| account_number | `string` | The unique number identifying the account (e.g., \"1234567890\"). |\n| bank_name | `string` | The name of the bank where the account is held (e.g., \"Access Bank Nigeria Plc\"). You can get the list of banks on the /banks endpoint. |\n| bank_code | `string` | The unique code identifying the bank (e.g., \"044\"). You can get the list of banks on the /banks endpoint. |\n| account_status | `string` | The status of the account (e.g., 1). Please see definition below. |\n| account_designation | `string` | The classification of the account holder (e.g., \"INDIVIDUAL\"). |\n| account_type | `string` | The type of account (e.g., \"SAVINGS\"). |\n\n#### Account Status\n\n| Status Code | Description |\n| --- | --- |\n| 1 | Active |\n| 2 | Dormant |\n| 3 | Closed |\n| 4 | PND (Post No Debit) |\n| 5 | PNC (Post No Credit) |\n| 6 | Inactive |\n| 7 | Total Freeze |\n| 8 | Other |"
							},
							"response": [
								{
									"name": "Complete BVN Accounts",
									"originalRequest": {
										"method": "PUT",
										"header": [],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"otp\": \"998278\"\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "https://adjutor.lendsqr.com/v2/verification/bvn/:bvn/accounts",
											"protocol": "https",
											"host": [
												"adjutor",
												"lendsqr",
												"com"
											],
											"path": [
												"v2",
												"verification",
												"bvn",
												":bvn",
												"accounts"
											],
											"variable": [
												{
													"key": "bvn",
													"value": ""
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 21 Feb 2024 07:30:41 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "1f01b79c-6b20-4fb8-b25c-b20a4b6efd6d"
										},
										{
											"key": "Last-Modified",
											"value": "Wed, 21 Feb 2024 07:30:32 GMT"
										},
										{
											"key": "ETag",
											"value": "W/\"74c-DjqwVcI8TtyBwlth2OV3gLYKrlQ\""
										},
										{
											"key": "CF-Cache-Status",
											"value": "DYNAMIC"
										},
										{
											"key": "Server",
											"value": "cloudflare"
										},
										{
											"key": "CF-RAY",
											"value": "858d48d90a446622-AMS"
										},
										{
											"key": "Content-Encoding",
											"value": "gzip"
										}
									],
									"cookie": [],
									"body": "{\n\t\"status\": \"success\",\n\t\"message\": \"Successful\",\n\t\"data\": [\n\t\t{\n\t\t\t\"account_name\": \"ADO JOHN SULE\",\n\t\t\t\"account_number\": \"9876543210\",\n\t\t\t\"bank_name\": \"GTBank\",\n\t\t\t\"bank_code\": \"058\",\n\t\t\t\"account_status\": 4,\n\t\t\t\"account_designation\": \"INDIVIDUAL\",\n\t\t\t\"account_type\": \"CURRENT\"\n\t\t},\n\t\t{\n\t\t\t\"account_name\": \"ADO JOHN SULE\",\n\t\t\t\"account_number\": \"1234567890\",\n\t\t\t\"bank_name\": \"Access Bank Nigeria Plc\",\n\t\t\t\"bank_code\": \"044\",\n\t\t\t\"account_status\": 1,\n\t\t\t\"account_designation\": \"INDIVIDUAL\",\n\t\t\t\"account_type\": \"SAVINGS\"\n\t\t}\n\t],\n\t\"meta\": {\n\t\t\"cost\": 20,\n\t\t\"balance\": 4735\n\t}\n}\n"
								}
							]
						}
					]
				},
				{
					"name": "Match Customer BVN Image",
					"request": {
						"method": "POST",
						"header": [],
						"body": {
							"mode": "raw",
							"raw": "{\n    \"image\": \"string\"\n}",
							"options": {
								"raw": {
									"language": "json"
								}
							}
						},
						"url": {
							"raw": "{{base_url}}verification/bvn/:bvn/selfies",
							"host": [
								"{{base_url}}verification"
							],
							"path": [
								"bvn",
								":bvn",
								"selfies"
							],
							"variable": [
								{
									"key": "bvn",
									"value": null
								}
							]
						},
						"description": "This endpoint allows for real-time verification of an individual's Bank Verification Number (BVN) through the comparison of their photograph and facial features with their BVN record, thereby providing an additional layer of security and accuracy in customer information validation.\n\n#### Payload\n\n`image`: `required` image URL\n\n#### Path Variables\n\n`bvn`: `required` BVN of the person with the image to be compared.\n\n#### Response fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| match | `boolean` | Indicates if a match was found (e.g., true) |\n| similarity | `float` | The percentage probability that the image compared are similar. The higher the number, the greater the chance of similarity (e.g., 99.95) |"
					},
					"response": [
						{
							"name": "Match customer BVN image",
							"originalRequest": {
								"method": "POST",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"image\": \"https://documents.lendsqr.com/irorun/45eab612ad3efff8f3da1e65130be8538b8fd6c8602da4252ec35c61ec18802b1619ba7eda625b3efb671bfc478cad84e834c5ad858722e993889b3xxxxxx.png\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}verification/bvn/:bvn/selfies",
									"host": [
										"{{base_url}}verification"
									],
									"path": [
										"bvn",
										":bvn",
										"selfies"
									],
									"variable": [
										{
											"key": "bvn",
											"value": "22536011111"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Thu, 10 Aug 2023 14:10:33 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json; charset=utf-8"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "X-Powered-By",
									"value": "Express"
								},
								{
									"key": "X-Request-ID",
									"value": "5314f877-acaf-4164-acb7-f1f99b3f1b0d"
								},
								{
									"key": "Last-Modified",
									"value": "Thu, 10 Aug 2023 14:10:32 GMT"
								},
								{
									"key": "ETag",
									"value": "W/\"82-9k7Nyc6Q89LGBa12YAMXH2UqqJs\""
								},
								{
									"key": "CF-Cache-Status",
									"value": "DYNAMIC"
								},
								{
									"key": "Server",
									"value": "cloudflare"
								},
								{
									"key": "CF-RAY",
									"value": "7f48d2a54d443d13-CDG"
								},
								{
									"key": "Content-Encoding",
									"value": "gzip"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"success\",\n    \"message\": \"Successful\",\n    \"data\": {\n        \"match\": true,\n        \"similarity\": 99.94831085205078\n    },\n    \"meta\": {\n        \"cost\": 30,\n        \"balance\": 1285\n    }\n}"
						}
					]
				},
				{
					"name": "Verify Customer Bank Account",
					"request": {
						"method": "POST",
						"header": [],
						"body": {
							"mode": "raw",
							"raw": "{\n    \"account_number\": \"number\",\n    \"bank_code\": \"number\"\n}",
							"options": {
								"raw": {
									"language": "json"
								}
							}
						},
						"url": {
							"raw": "{{base_url}}verification/bankaccount",
							"host": [
								"{{base_url}}verification"
							],
							"path": [
								"bankaccount"
							]
						},
						"description": "This endpoint is used for verification of a customer's bank account.\n\n#### Payload\n\n`account_number`: `required` account number to be verified\n\n`bank_code`: `required` the bank code for the account number\n\n#### Response Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| bank_code | `string` | Central Bank of Nigeria code identifying the bank (e.g., \"058\") |\n| bank_name | `string` | Name of the bank (e.g., \"Example Bank Plc\") |\n| account_name | `string` | Name associated with the account (e.g., \"DOE JOHN\") |\n| account_number | `string` | Account number (e.g., \"0425571111\") |\n| bvn | `string` | Bank Verification Number. The middle 7 numbers are masked with 0s (e.g., \"22000000021\") |"
					},
					"response": [
						{
							"name": "Verify Customer Bank Account",
							"originalRequest": {
								"method": "POST",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"account_number\": \"0425571111\",\n    \"bank_code\": \"058\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}verification/bankaccount/bvn",
									"host": [
										"{{base_url}}verification"
									],
									"path": [
										"bankaccount",
										"bvn"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Thu, 10 Aug 2023 14:43:21 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json; charset=utf-8"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "X-Powered-By",
									"value": "Express"
								},
								{
									"key": "X-Request-ID",
									"value": "45a5849d-e413-474f-966d-ac800803a5f8"
								},
								{
									"key": "Last-Modified",
									"value": "Thu, 10 Aug 2023 14:43:21 GMT"
								},
								{
									"key": "ETag",
									"value": "W/\"c9-19Gwq+rB7O302vWla1jPDh/+TTI\""
								},
								{
									"key": "CF-Cache-Status",
									"value": "DYNAMIC"
								},
								{
									"key": "Server",
									"value": "cloudflare"
								},
								{
									"key": "CF-RAY",
									"value": "7f4902b9bb13046b-CDG"
								},
								{
									"key": "Content-Encoding",
									"value": "gzip"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"success\",\n    \"message\": \"Successful\",\n    \"data\": {\n        \"bank_code\": \"058\",\n        \"account_name\": \"DOE JOHN\",\n        \"account_number\": \"0425571111\",\n        \"bvn\": \"22000000021\"\n    },\n    \"meta\": {\n        \"cost\": 10,\n        \"balance\": 1245\n    }\n}"
						}
					]
				},
				{
					"name": "Check Karma for Customer",
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "{{base_url}}verification/karma/:identity",
							"host": [
								"{{base_url}}verification"
							],
							"path": [
								"karma",
								":identity"
							],
							"variable": [
								{
									"key": "identity",
									"value": ""
								}
							]
						},
						"description": "Karma is a database of blacklisted bad actors within the Lendsqr ecosystem. A bad actor is someone who has been involved with fraud or has tried to request loans with fake identity. A bad actor may also be a chronic defaulter whose loan has been written off.\n\nThis endpoint is used to check if a customer is on the blacklist of bad actors.\n\n#### Path Variables\n\n`identity`: `required` Identity of customer which could be one of the following:\n\n| Field | Description | Format Example |\n| --- | --- | --- |\n| Email Address | Format should be in the form of [email@example.com](https://mailto:email@example.com) | [email@example.com](https://mailto:email@example.com) |\n| Phone Number | Format should be in the form of +2347012345678 | +2347012345678 |\n| Domain Name | Format should be in the form of example.com | example.com |\n| BVN | Format should be in the form of 22212345678 | 22212345678 |\n| NUBAN Account number | Format should be in the form of XXX-1234567890 Where XXX is the CBN bank code | 070-1234567890 for a Fidelity Bank account. |\n| Images | Format is Base64 | Base64 encoded string |\n\n#### Response Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| karma_identity | `string` | Unique identifier for karma (e.g., \"0zspgifzbo.ga\") |\n| amount_in_contention | `string` | Amount involved in contention (e.g., \"0.00\") |\n| reason | `string` | Reason for the karma entry, if applicable (e.g., null) |\n| default_date | `date` | Date of default (e.g., \"2020-05-18\") |\n| karma_type | `object` | Type of karma (e.g., {\"karma\": \"Others\"}) |\n| karma_identity_type | `object` | Type of identity associated with karma (e.g., {\"identity_type\": \"Domain\"}) |\n| reporting_entity | `object` | Entity reporting the karma (e.g., {\"name\": \"Blinkcash\", \"email\": \"[support@blinkcash.ng](https://mailto:support@blinkcash.ng)\"}) |"
					},
					"response": [
						{
							"name": "Check Karma for Customer",
							"originalRequest": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}verification/karma/:identity",
									"host": [
										"{{base_url}}verification"
									],
									"path": [
										"karma",
										":identity"
									],
									"variable": [
										{
											"key": "identity",
											"value": "0zspgifzbo.ga"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Tue, 08 Aug 2023 14:26:38 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json; charset=utf-8"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "X-Powered-By",
									"value": "Express"
								},
								{
									"key": "X-Request-ID",
									"value": "0150a3b9-1e2e-4bc1-825e-f4bb024f7463"
								},
								{
									"key": "Last-Modified",
									"value": "Tue, 08 Aug 2023 14:26:38 GMT"
								},
								{
									"key": "ETag",
									"value": "W/\"157-/X62qo9vh7N9XNeVvLk5BxWrnvs\""
								},
								{
									"key": "CF-Cache-Status",
									"value": "DYNAMIC"
								},
								{
									"key": "Server",
									"value": "cloudflare"
								},
								{
									"key": "CF-RAY",
									"value": "7f386f7a0fc9d430-LOS"
								},
								{
									"key": "Content-Encoding",
									"value": "gzip"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"success\",\n    \"message\": \"Successful\",\n    \"data\": {\n        \"karma_identity\": \"0zspgifzbo.ga\",\n        \"amount_in_contention\": \"0.00\",\n        \"reason\": null,\n        \"default_date\": \"2020-05-18\",\n        \"karma_type\": {\n            \"karma\": \"Others\"\n        },\n        \"karma_identity_type\": {\n            \"identity_type\": \"Domain\"\n        },\n        \"reporting_entity\": {\n            \"name\": \"Blinkcash\",\n            \"email\": \"support@blinkcash.ng\"\n        }\n    },\n    \"meta\": {\n        \"cost\": 10,\n        \"balance\": 1600\n    }\n}"
						}
					]
				},
				{
					"name": "Check for Borrower on Ecosystem",
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "{{base_url}}verification/ecosystem/:bvn",
							"host": [
								"{{base_url}}verification"
							],
							"path": [
								"ecosystem",
								":bvn"
							],
							"variable": [
								{
									"key": "bvn",
									"value": null,
									"description": "Bank Verification Number"
								}
							]
						},
						"description": "The Lendsqr ecosystem provides an aggregated view of borrowers which lenders could have access to make decisions. To access this service, the lender must provide an evidence of customer explicit consent.\n\nFurthermore, where it is proven that a consent was never provided, the lender would be liable for all legal cost required to ameliorate issues that may arise. Lender may also be removed from the platform.\n\nThis endpoint is used to verify if a borrower exists on the Lendsqr ecosystem.\n\n#### Path Variables\n\n`bvn`: `required` BVN no. of the person to be checked.\n\n#### Response Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| bvn | `string` | Bank Verification Number (e.g., \"22536011111\") |\n| first_name | `string` | First name of the individual (e.g., \"JANE\") |\n| last_name | `string` | Last name of the individual (e.g., \"DOE\") |\n| bvn_phone_number | `string` | Phone number registered with BVN (e.g., \"07062561111\") |\n| date_of_birth | `date` | Date of birth in ISO format (e.g., \"1997-09-10\") |\n| age | `integer` | Age of the individual (e.g., 25) |\n| unique_phone_numbers | `integer` | Count of unique phone numbers (e.g., 0) |\n| phone_number | `string` | Primary phone number (e.g., \"07062561111\") |\n| unique_emails | `integer` | Count of unique email addresses (e.g., 0) |\n| email | `string` | Email address (e.g., \"[janedoe@gmail.com](https://mailto:janedoe@gmail.com)\") |\n| gender | `string` | Gender of the individual (e.g., \"Female\") |\n| lenders | `integer` | Number of lenders interacted with (e.g., 1) |\n| first_account | `date` | Date of first account creation in ISO format (e.g., \"2020-11-16\") |\n| last_account | `date` | Date of last account creation in ISO format (e.g., \"2023-06-26\") |\n| failed_selfie_bvn_check | `integer` | Number of failed BVN selfie checks (e.g., 0) |\n| lending_lenders | `integer` | Number of lending lenders (e.g., 0) |\n| loans | `integer` | Total number of loans (e.g., 0) |\n| loan_amount | `integer` | Total loan amount (e.g., 0) |\n| loan_amount_minimum | `integer` | Minimum loan amount (e.g., 0) |\n| loan_amount_maximum | `integer` | Maximum loan amount (e.g., 150000) |\n| loan_amount_average | `float` | Average loan amount (e.g., 5892.954545) |\n| settled_loans | `integer` | Number of settled loans (e.g., 0) |\n| settled_loan_amount | `integer` | Amount of settled loans (e.g., 0) |\n| settled_loan_amount_paid | `integer` | Amount paid for settled loans (e.g., 0) |\n| running_loans | `integer` | Number of running loans (e.g., 0) |\n| running_loan_amount | `integer` | Amount of running loans (e.g., 0) |\n| past_due_loans | `integer` | Number of past due loans (e.g., 0) |\n| past_due_loan_amount | `integer` | Amount of past due loans (e.g., 0) |\n| past_due_loan_amount_due | `integer` | Amount due for past due loans (e.g., 2000) |\n| penalty | `integer` | Penalty amount (e.g., 0) |\n| penalty_paid | `integer` | Penalty amount paid (e.g., 0) |\n| delayed_paid_loans | `integer` | Number of delayed paid loans (e.g., 0) |\n| delayed_paid_loan_amount | `integer` | Amount of delayed paid loans (e.g., 0) |\n| delayed_paid_loans_trials | `integer` | Trials for delayed paid loans (e.g., 0) |\n| delayed_paid_loans_avg | `integer` | Average trials for delayed paid loans (e.g., 0) |\n| delayed_paid_loans_trials_max | `integer` | Maximum trials for delayed paid loans (e.g., 0) |\n| delayed_paid_loans_trials_min | `integer` | Minimum trials for delayed paid loans (e.g., 0) |\n| first_loan_date | `date` | Date of first loan in ISO format (e.g., \"2020-12-24\") |\n| last_loan_date | `date` | Date of last loan in ISO format (e.g., \"2023-07-20\") |\n| loan_requests | `integer` | Number of loan requests (e.g., 0) |\n| failed_loan_requests | `integer` | Number of failed loan requests (e.g., 0) |\n| logins | `integer` | Number of logins (e.g., 115) |\n| first_login | `date` | Date of first login in ISO format (e.g., \"2023-06-01\") |\n| last_login | `date` | Date of last login in ISO format (e.g., \"2023-08-08\") |\n| unique_login_ips | `integer` | Count of unique login IPs (e.g., 0) |\n| unique_device_ids | `integer` | Count of unique device IDs (e.g., 0) |\n| distinct_mobile_os | `integer` | Count of distinct mobile OS used (e.g., 0) |\n| duplicated_devices | `integer` | Count of duplicated devices (e.g., 0) |\n| shared_device_users | `integer` | Count of shared device users (e.g., 0) |\n| credit_delinquency | `integer` | Credit delinquency flag (e.g., 0) |\n| processed_on | `date` | Date when the data was processed in ISO format (e.g., \"2023-08-08\") |"
					},
					"response": [
						{
							"name": "Check for Borrower on Ecosystem",
							"originalRequest": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}verification/ecosystem/:bvn",
									"host": [
										"{{base_url}}verification"
									],
									"path": [
										"ecosystem",
										":bvn"
									],
									"variable": [
										{
											"key": "bvn",
											"value": "22153475955"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Tue, 08 Aug 2023 14:28:56 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json; charset=utf-8"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "X-Powered-By",
									"value": "Express"
								},
								{
									"key": "X-Request-ID",
									"value": "a7855073-2a36-4924-a21f-077ef89219c0"
								},
								{
									"key": "Last-Modified",
									"value": "Tue, 08 Aug 2023 14:28:55 GMT"
								},
								{
									"key": "ETag",
									"value": "W/\"591-Cd5yroepYTa3PyDTbhzMyhKotAE\""
								},
								{
									"key": "CF-Cache-Status",
									"value": "DYNAMIC"
								},
								{
									"key": "Server",
									"value": "cloudflare"
								},
								{
									"key": "CF-RAY",
									"value": "7f3872d4eeb8d430-LOS"
								},
								{
									"key": "Content-Encoding",
									"value": "gzip"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"success\",\n    \"message\": \"Successful\",\n    \"data\": {\n        \"bvn\": \"22536011111\",\n        \"first_name\": \"JANE\",\n        \"last_name\": \"DOE\",\n        \"bvn_phone_number\": \"07062561111\",\n        \"date_of_birth\": \"1997-09-10T00:00:00.000Z\",\n        \"age\": 25,\n        \"unique_phone_numbers\": 0,\n        \"phone_number\": \"07062561111\",\n        \"unique_emails\": 0,\n        \"email\": \"janedoe@gmail.com\",\n        \"gender\": \"Female\",\n        \"lenders\": 1,\n        \"first_account\": \"2020-11-16T10:49:57.000Z\",\n        \"last_account\": \"2023-06-26T07:56:37.000Z\",\n        \"failed_selfie_bvn_check\": 0,\n        \"lending_lenders\": 0,\n        \"loans\": 0,\n        \"loan_amount\": 0,\n        \"loan_amount_minimum\": 0,\n        \"loan_amount_maximum\": 150000,\n        \"loan_amount_average\": 5892.954545,\n        \"settled_loans\": 0,\n        \"settled_loan_amount\": 0,\n        \"settled_loan_amount_paid\": 0,\n        \"running_loans\": 0,\n        \"running_loan_amount\": 0,\n        \"past_due_loans\": 0,\n        \"past_due_loan_amount\": 0,\n        \"past_due_loan_amount_due\": 2000,\n        \"penalty\": 0,\n        \"penalty_paid\": 0,\n        \"delayed_paid_loans\": 0,\n        \"delayed_paid_loan_amount\": 0,\n        \"delayed_paid_loans_trials\": 0,\n        \"delayed_paid_loans_avg\": 0,\n        \"delayed_paid_loans_trials_max\": 0,\n        \"delayed_paid_loans_trials_min\": 0,\n        \"first_loan_date\": \"2020-12-24T07:54:37.000Z\",\n        \"last_loan_date\": \"2023-07-20T11:38:02.000Z\",\n        \"loan_requests\": 0,\n        \"failed_loan_requests\": 0,\n        \"logins\": 115,\n        \"first_login\": \"2023-06-01T12:32:27.000Z\",\n        \"last_login\": \"2023-08-08T08:23:49.000Z\",\n        \"unique_login_ips\": 0,\n        \"unique_device_ids\": 0,\n        \"distinct_mobile_os\": 0,\n        \"duplicated_devices\": 0,\n        \"shared_device_users\": 0,\n        \"credit_delinquency\": 0,\n        \"processed_on\": \"2023-08-08T14:02:33.000Z\"\n    },\n    \"meta\": {\n        \"cost\": 25,\n        \"balance\": 1590\n    }\n}"
						}
					]
				},
				{
					"name": "Verify Custormer NIN",
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "{{base_url}}verification/nin/:nin",
							"host": [
								"{{base_url}}verification"
							],
							"path": [
								"nin",
								":nin"
							],
							"variable": [
								{
									"key": "nin",
									"value": ""
								}
							]
						},
						"description": "This endpoint allows for real-time verification of an individual's National Identification Number (NIN) , thereby providing an additional layer of security and accuracy in customer information validation.\n\n#### Path Variables\n\nnin: `required` NIN of the person to be checked.\n\n#### Response Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| nin | `string` | Bank Verification Number (e.g., \"70123456789\") |\n| first_name | `string` | First name of the individual (e.g., \"John\") |\n| middle_name | `string` | Middle name of the individual (e.g., \"Frank\") |\n| last_name | `string` | Last name of the individual (e.g., \"Doe\") |\n| dob | `date` | Date of birth in ISO format (e.g., \"1997-09-10\") |\n| mobile | `string` | Primary phone number (e.g., \"08081234561\") |\n| registration_date | `string` | User NIN registeration date in ISO format (e.g., \"2020-01-01\") |\n| email | `string` | Email address (e.g., \"[johndoe@example.com](https://mailto:johndoe@example.com)\") |\n| gender | `string` | Gender of the individual (e.g., \"Female\") |\n| marital_status | `string` | Marital Status of the individual (e.g., \"Single\") |\n| state_of_residence | `string` | State of Residence of the individual (e.g., \"Lagos\") |\n| image_url | `string` | NIN Image Url (e.g. [https://documents.lendsqr.com/image_url.png](https://documents.lendsqr.com/image_url.png)) |"
					},
					"response": [
						{
							"name": "Verify Custormer NIN",
							"originalRequest": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}verification/nin/:nin",
									"host": [
										"{{base_url}}verification"
									],
									"path": [
										"nin",
										":nin"
									],
									"variable": [
										{
											"key": "nin",
											"value": "70123456789",
											"description": "National Identity Number"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Tue, 08 Aug 2023 14:28:56 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json; charset=utf-8"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "X-Powered-By",
									"value": "Express"
								},
								{
									"key": "X-Request-ID",
									"value": "a7855073-2a36-4924-a21f-077ef89219c0"
								},
								{
									"key": "Last-Modified",
									"value": "Tue, 08 Aug 2023 14:28:55 GMT"
								},
								{
									"key": "ETag",
									"value": "W/\"591-Cd5yroepYTa3PyDTbhzMyhKotAE\""
								},
								{
									"key": "CF-Cache-Status",
									"value": "DYNAMIC"
								},
								{
									"key": "Server",
									"value": "cloudflare"
								},
								{
									"key": "CF-RAY",
									"value": "7f3872d4eeb8d430-LOS"
								},
								{
									"key": "Content-Encoding",
									"value": "gzip"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"success\",\n    \"message\": \"Successful\",\n    \"data\": {\n        \"nin\": \"70123456789\",\n        \"first_name\": \"John\",\n        \"middle_name\": \"Doe\",\n        \"last_name\": \"Frank\",\n        \"dob\": \"1982-01-01\",\n        \"formatted_dob\": \"1982-01-01\",\n        \"mobile2\": \"08081234561\",\n        \"mobile\": \"08081234561\",\n        \"registration_date\": \"2020-01-01\",\n        \"email\": \"email@example.com\",\n        \"gender\": \"Male\",\n        \"marital_status\": \"single\",\n        \"state_of_residence\": \"lagos\",\n        \"base64Image\": \"[base64Image]\",\n        \"image_url\": \"https://documents.lendsqr.com/image_url.png\"\n    },\n    \"meta\": {\n        \"cost\": 45,\n        \"balance\": 3435\n    }\n}"
						}
					]
				}
			],
			"description": "The Validation APIs are resources and tools for validating customer information. These validation processes make use of APIs that allow you to confirm the accuracy of customer information using their Bank Verification Numbers (BVNs), email addresses, or phone numbers.\n\nThe APIs are designed to help you ensure that customer information is accurate and up-to-date, providing you with a reliable and efficient method for validating customer data."
		},
		{
			"name": "Credit Bureaus",
			"item": [
				{
					"name": "Get Credit Report from CRC Credit Bureau",
					"protocolProfileBehavior": {
						"disableBodyPruning": true
					},
					"request": {
						"method": "GET",
						"header": [],
						"body": {
							"mode": "raw",
							"raw": ""
						},
						"url": {
							"raw": "{{base_url}}creditbureaus/crc/:bvn",
							"host": [
								"{{base_url}}creditbureaus"
							],
							"path": [
								"crc",
								":bvn"
							],
							"variable": [
								{
									"key": "bvn",
									"value": "",
									"description": "This must be a valid Bank Verification Number"
								}
							]
						},
						"description": "This request is used to check the CRC database for the credit history of a customer using their BVN.\n\n#### Path Variables\n\n`bvn`: `required` The BVN of the customer."
					},
					"response": [
						{
							"name": "Get Credit Report from CRC Credit Bureau",
							"originalRequest": {
								"method": "GET",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": ""
								},
								"url": {
									"raw": "{{base_url}}creditbureaus/crc/:bvn",
									"host": [
										"{{base_url}}creditbureaus"
									],
									"path": [
										"crc",
										":bvn"
									],
									"variable": [
										{
											"key": "bvn",
											"value": "22293381111"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Tue, 08 Aug 2023 14:45:13 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json; charset=utf-8"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "X-Powered-By",
									"value": "Express"
								},
								{
									"key": "X-Request-ID",
									"value": "b0a64f17-3b9c-486a-bcd9-238c74c8dc6b"
								},
								{
									"key": "Last-Modified",
									"value": "Tue, 08 Aug 2023 14:45:11 GMT"
								},
								{
									"key": "ETag",
									"value": "W/\"3a9-O71eH/thvISxq/G7zT9AeNi1Bl4\""
								},
								{
									"key": "CF-Cache-Status",
									"value": "DYNAMIC"
								},
								{
									"key": "Server",
									"value": "cloudflare"
								},
								{
									"key": "CF-RAY",
									"value": "7f388aa9590fc4fc-LOS"
								},
								{
									"key": "Content-Encoding",
									"value": "gzip"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"success\",\n    \"message\": \"Successful\",\n    \"data\": {\n        \"consdisclaimer\": {\n            \"getdisclaimercontent\": {\n                \"_x0031_\": \"1\"\n            }\n        },\n        \"consumer_relation\": \"\",\n        \"last_checked_date\": \"2023-06-29 12:00:40\",\n        \"credit_nano_summary\": {\n            \"summary\": {\n                \"last_reported_date\": \"31-MAY-2023\",\n                \"has_creditfacilities\": \"YES\",\n                \"no_of_delinqcreditfacilities\": \"2\"\n            }\n        },\n        \"mfcredit_nano_summary\": {\n            \"summary\": {\n                \"last_reported_date\": \"31-MAY-2023\",\n                \"has_creditfacilities\": \"YES\",\n                \"no_of_delinqcreditfacilities\": \"1\"\n            }\n        },\n        \"mgcredit_nano_summary\": {\n            \"summary\": {\n                \"has_creditfacilities\": \"NO\",\n                \"no_of_delinqcreditfacilities\": \"0\"\n            }\n        },\n        \"nano_consumer_profile\": {\n            \"consumer_details\": {\n                \"name\": \"JOHN DOE\",\n                \"ruid\": \"1112020002201111\",\n                \"gender\": \"001\",\n                \"last_name\": \"DOE\",\n                \"first_name\": \"JOHN\",\n                \"citizenship\": \"NG\",\n                \"date_of_birth\": \"01-OCT-1960\",\n                \"identification\": {\n                    \"ruid\": \"1112020002201111\",\n                    \"id_value\": \"22293381111\",\n                    \"source_id\": \"BVN\",\n                    \"id_display_name\": \"Business Verification Number\"\n                }\n            }\n        }\n    },\n    \"meta\": {\n        \"cost\": 100,\n        \"balance\": 1355\n    }\n}"
						}
					]
				},
				{
					"name": "Get Credit Report from FirstCentral Credit Bureau",
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "{{base_url}}creditbureaus/firstcentral/:bvn",
							"host": [
								"{{base_url}}creditbureaus"
							],
							"path": [
								"firstcentral",
								":bvn"
							],
							"variable": [
								{
									"key": "bvn",
									"value": "",
									"description": "This must be a valid Bank Verification Number"
								}
							]
						},
						"description": "This request is used to check the CRC database for the credit history of a customer using their BVN.\n\n#### Path Variables\n\n`bvn`: `required` The BVN of the customer."
					},
					"response": [
						{
							"name": "Get Credit Report from FirstCentral Credit Bureau",
							"originalRequest": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}creditbureaus/firstcentral/:bvn",
									"host": [
										"{{base_url}}creditbureaus"
									],
									"path": [
										"firstcentral",
										":bvn"
									],
									"variable": [
										{
											"key": "bvn",
											"value": "22293381111"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Mon, 14 Aug 2023 13:26:10 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json; charset=utf-8"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "X-Powered-By",
									"value": "Express"
								},
								{
									"key": "X-Request-ID",
									"value": "215fcd37-0d7f-4fc8-9031-7fa20e55bad0"
								},
								{
									"key": "Last-Modified",
									"value": "Mon, 14 Aug 2023 13:26:10 GMT"
								},
								{
									"key": "ETag",
									"value": "W/\"5da-eIapFMBHh+VQsgkRqx4HYnwZad4\""
								},
								{
									"key": "CF-Cache-Status",
									"value": "DYNAMIC"
								},
								{
									"key": "Server",
									"value": "cloudflare"
								},
								{
									"key": "CF-RAY",
									"value": "7f698727981103d6-LIS"
								},
								{
									"key": "Content-Encoding",
									"value": "gzip"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"success\",\n    \"message\": \"Successful\",\n    \"data\": [\n        {\n            \"SubjectList\": [\n                {\n                    \"Reference\": \"2663443\",\n                    \"ConsumerID\": \"2663443\",\n                    \"SearchOutput\": \"DOE JANE, dantata estate kubwa abuja\"\n                }\n            ]\n        },\n        {\n            \"PersonalDetailsSummary\": [\n                {\n                    \"Gender\": \"Female\",\n                    \"Header\": \"PERSONAL DETAILS SUMMARY: DOE JANE\",\n                    \"Surname\": \"DOE\",\n                    \"BirthDate\": \"19/03/1997\",\n                    \"FirstName\": \"JANE\",\n                    \"OtheridNo\": \"\",\n                    \"CellularNo\": \"2348169591111\",\n                    \"ConsumerID\": \"2663443\",\n                    \"Dependants\": \"0\",\n                    \"OtherNames\": \"\",\n                    \"PassportNo\": null,\n                    \"PencomIDNo\": \"\",\n                    \"Nationality\": \"Nigeria\",\n                    \"ReferenceNo\": null,\n                    \"EmailAddress\": \"\",\n                    \"NationalIDNo\": \"\",\n                    \"MaritalStatus\": null,\n                    \"EmployerDetail\": null,\n                    \"PostalAddress1\": \"DANTATA ESTATE ABUJA FEDERAL CAPITAL TERRITORY\",\n                    \"PostalAddress2\": \"15\",\n                    \"PostalAddress3\": \"\",\n                    \"PostalAddress4\": \" Nigeria\",\n                    \"HomeTelephoneNo\": \"2348169591111\",\n                    \"WorkTelephoneNo\": \"2348169591111\",\n                    \"DriversLicenseNo\": null,\n                    \"PropertyOwnedType\": \"\",\n                    \"BankVerificationNo\": \"22293381111\",\n                    \"ResidentialAddress1\": \"10nasiru dantata estate kubwa abuja\",\n                    \"ResidentialAddress2\": \"\",\n                    \"ResidentialAddress3\": \"\",\n                    \"ResidentialAddress4\": \" \"\n                }\n            ]\n        },\n        {\n            \"CreditSummary\": [\n                {\n                    \"NumberofAccountsInBadStanding\": \"0\",\n                    \"TotalNumberOfAccountsReported\": \"6\",\n                    \"NumberOfAccountsInGoodStanding\": \"6\"\n                }\n            ]\n        },\n        {\n            \"PerformanceClassification\": [\n                {\n                    \"NoOfLoansLost\": \"0\",\n                    \"NoOfLoansDoubtful\": \"0\",\n                    \"NoOfLoansPerforming\": \"6\",\n                    \"NoOfLoansSubstandard\": \"1\"\n                }\n            ]\n        },\n        {\n            \"EnquiryDetails\": [\n                {\n                    \"ProductID\": \"63\",\n                    \"MatchingRate\": \"90\",\n                    \"SubscriberEnquiryEngineID\": \"179484634\",\n                    \"SubscriberEnquiryResultID\": \"22059650\"\n                }\n            ]\n        }\n    ],\n    \"meta\": {\n        \"cost\": 100,\n        \"balance\": 1025\n    }\n}"
						}
					]
				}
			],
			"description": "The Credit Bureaus folder contains resources and tools for accessing credit information through credit bureau integrations."
		},
		{
			"name": "Decisioning",
			"item": [
				{
					"name": "Get Decision Models",
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "{{base_url}}decisioning/models",
							"host": [
								"{{base_url}}decisioning"
							],
							"path": [
								"models"
							]
						},
						"description": "This endpoint fetches all the decision models that have been configured for your profile. This would allow you to programmatically iterate and select."
					},
					"response": []
				},
				{
					"name": "Get Decision Model Details",
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "{{base_url}}decisioning/models/:id/settings",
							"host": [
								"{{base_url}}decisioning"
							],
							"path": [
								"models",
								":id",
								"settings"
							],
							"variable": [
								{
									"key": "id",
									"value": null
								}
							]
						},
						"description": "This endpoint is used to obtain the details of a Decision Model.\n\n#### Path Variables\n\n`id`: `required` The id of the decison model.decision"
					},
					"response": []
				},
				{
					"name": "Oraculi Borrower Scoring",
					"request": {
						"method": "POST",
						"header": [],
						"body": {
							"mode": "raw",
							"raw": "{\n    \"gender\": \"Female\",\n    \"marital_status\": \"Single\",\n    \"age\": \"21 - 30\",\n    \"location\": \"lagos\",\n    \"no_of_dependent\": \"0\",\n    \"type_of_residence\": \"Rented Apartment\",\n    \"educational_attainment\": \"BSc, HND and Other Equivalent\",\n    \"employment_status\": \"Employed\",\n    \"sector_of_employment\": \"Other Financial\",\n    \"tier\": \"Tier 1\",\n    \"monthly_net_income\": \"100,000 - 199,999\",\n    \"employer_category\": \"Private Company\",\n    \"bvn\": \"22233312345\",\n    \"phone_number\": \"08012345678\",\n    \"total_years_of_experience\": 5,\n    \"time_with_current_employer\": 2,\n    \"previous_lendsqr_loans\": 3,\n    \"code\": \"9dppknauu\",\n    \"phone\": \"08012345678\",\n    \"bvn_phone\": \"08012345678\",\n    \"office_email\": \"adojohnsule@lendsqr.com\",\n    \"personal_email\": \"adojohnsule@lendsqr.com\",\n    \"amount\": 10000\n}",
							"options": {
								"raw": {
									"language": "json"
								}
							}
						},
						"url": {
							"raw": "{{base_url}}decisioning/models/:id",
							"host": [
								"{{base_url}}decisioning"
							],
							"path": [
								"models",
								":id"
							],
							"variable": [
								{
									"key": "id",
									"value": "2355"
								}
							]
						},
						"description": "This endpoint is used for scoring based on the passed parameters.\n\nThe Lendsqr data provides the source of data that have been used to develop and optimize our proprietary scoring algorithms. The scoring system is continually updated to reflect new insights into the shifting borrower’s behaviors both for cohorts of customers and for the Nigerian financial system. The ID variable refers to the ID of the decision model.\n\n#### Request Payload\n\n| Property | Type | Examples |\n| --- | --- | --- |\n| `gender` | `string` | male, female |\n| `marital_status` | `string` | married, single, divorced, separated, widowed |\n| `age` | integer | 25, 37 |\n| `location` | `string` | Lagos, Ibadan |\n| `no_of_dependent` | integer | 0, 5 |\n| `type_of_residence` | `string` | own house, rented apartment, parents apartment |\n| `education_attainment` | `string` | MSc and above, BSc, HND and Other Equivalent, Diploma/School Cert, Others |\n| `employment_status` | `string` | employed, self employed, unemployed, retired |\n| `sector_of_employment` | `string` | agriculture, banking, education, law |\n| `tier` | `string` | tier 1. tier 2 |\n| `monthly_net_income` | `string` | 700,000 -999,999, above 1,000,000, |\n| `employment_category` | `string` | artisan, enterprise, private company, federal: public |\n| `bvn` | `string` | 22222222222 |\n| `phone_number` | `string` | 0805555555 |\n| `working_period` | integer | 1 |\n| `time_with_current_employer` | integer | 1 |\n| `previous_lendsqr_loans` | integer | 1 |\n| `code` | `string` | 56etruu |\n| `phone` | `string` | 08106666666 |\n| `bvn_phone` | `string` | 08106666666 |\n| `official_email` | `string` | [male@female.com](https://) |\n| `personal_email` | `string` | [male@female.com](https://) |\n| `amount` | `string` | 5000 |"
					},
					"response": [
						{
							"name": "Oraculli Borrower Scoring",
							"originalRequest": {
								"method": "POST",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"gender\": \"Female\",\n    \"marital_status\": \"Single\",\n    \"age\": \"21\",\n    \"location\": \"lagos\",\n    \"no_of_dependent\": \"0\",\n    \"type_of_residence\": \"Rented Apartment\",\n    \"educational_attainment\": \"BSc, HND and Other Equivalent\",\n    \"employment_status\": \"Employed\",\n    \"sector_of_employment\": \"Other Financial\",\n    \"monthly_net_income\": \"100,000 - 199,999\",\n    \"employer_category\": \"Private Company\",\n    \"bvn\": \"22536051111\",\n    \"phone_number\": \"08012345678\",\n    \"total_years_of_experience\": 5,\n    \"time_with_current_employer\": 2,\n    \"previous_lendsqr_loans\": 3,\n    \"phone\": \"07062561111\",\n    \"bvn_phone\": \"07062561111\",\n    \"office_email\": \"adojohnsule@lendsqr.com\",\n    \"personal_email\": \"adojohnsule@lendsqr.com\",\n    \"amount\": 10000\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}decisioning/models/:id",
									"host": [
										"{{base_url}}decisioning"
									],
									"path": [
										"models",
										":id"
									],
									"variable": [
										{
											"key": "id",
											"value": "2355"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Tue, 08 Aug 2023 14:42:46 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json; charset=utf-8"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "X-Powered-By",
									"value": "Express"
								},
								{
									"key": "X-Request-ID",
									"value": "4e829b52-a39b-4fad-8da8-93d9ea8171ab"
								},
								{
									"key": "Last-Modified",
									"value": "Tue, 08 Aug 2023 14:42:45 GMT"
								},
								{
									"key": "ETag",
									"value": "W/\"7f6-IOxnW/y6JbsKwgsmXd4jlYoR2sc\""
								},
								{
									"key": "CF-Cache-Status",
									"value": "DYNAMIC"
								},
								{
									"key": "Server",
									"value": "cloudflare"
								},
								{
									"key": "CF-RAY",
									"value": "7f3887169982c4fc-LOS"
								},
								{
									"key": "Content-Encoding",
									"value": "gzip"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"success\",\n    \"message\": \"Successful\",\n    \"data\": {\n        \"credit_score_items\": [\n            {\n                \"score_name\": \"age\",\n                \"score_value\": \"21\",\n                \"weight\": \"7\",\n                \"maximum_score\": 10,\n                \"borrower_score\": 6,\n                \"weighted_score\": 0.0382\n            },\n            {\n                \"score_name\": \"gender\",\n                \"score_value\": \"Female\",\n                \"weight\": \"10\",\n                \"maximum_score\": 10,\n                \"borrower_score\": 10,\n                \"weighted_score\": 0.0909\n            },\n            {\n                \"score_name\": \"location\",\n                \"score_value\": \"lagos\",\n                \"weight\": \"5\",\n                \"maximum_score\": 10,\n                \"borrower_score\": 9,\n                \"weighted_score\": 0.0409\n            },\n            {\n                \"score_name\": \"customer_tier\",\n                \"score_value\": null,\n                \"weight\": \"5\",\n                \"maximum_score\": 10,\n                \"borrower_score\": 0,\n                \"weighted_score\": 0\n            },\n            {\n                \"score_name\": \"marital_status\",\n                \"score_value\": \"Single\",\n                \"weight\": \"5\",\n                \"maximum_score\": 10,\n                \"borrower_score\": 6,\n                \"weighted_score\": 0.0273\n            },\n            {\n                \"score_name\": \"employer_category\",\n                \"score_value\": \"Private Company\",\n                \"weight\": \"5\",\n                \"maximum_score\": 10,\n                \"borrower_score\": 8,\n                \"weighted_score\": 0.0364\n            },\n            {\n                \"score_name\": \"employment_status\",\n                \"score_value\": \"Employed\",\n                \"weight\": \"10\",\n                \"maximum_score\": 10,\n                \"borrower_score\": 10,\n                \"weighted_score\": 0.0909\n            },\n            {\n                \"score_name\": \"type_of_residence\",\n                \"score_value\": \"Rented Apartment\",\n                \"weight\": \"5\",\n                \"maximum_score\": 10,\n                \"borrower_score\": 10,\n                \"weighted_score\": 0.0455\n            },\n            {\n                \"score_name\": \"monthly_net_income\",\n                \"score_value\": \"100,000 - 199,999\",\n                \"weight\": \"10\",\n                \"maximum_score\": 10,\n                \"borrower_score\": 5,\n                \"weighted_score\": 0.0455\n            },\n            {\n                \"score_name\": \"no_of_dependent\",\n                \"score_value\": \"0\",\n                \"weight\": \"8\",\n                \"maximum_score\": 10,\n                \"borrower_score\": 5,\n                \"weighted_score\": 0.0364\n            },\n            {\n                \"score_name\": \"sector_of_employment\",\n                \"score_value\": \"Other Financial\",\n                \"weight\": \"5\",\n                \"maximum_score\": 10,\n                \"borrower_score\": 6,\n                \"weighted_score\": 0.0273\n            },\n            {\n                \"score_name\": \"educational_attainment\",\n                \"score_value\": \"BSc, HND and Other Equivalent\",\n                \"weight\": \"5\",\n                \"maximum_score\": 10,\n                \"borrower_score\": 8,\n                \"weighted_score\": 0.0364\n            },\n            {\n                \"score_name\": \"time_with_current_employer\",\n                \"score_value\": 2,\n                \"weight\": \"5\",\n                \"maximum_score\": 10,\n                \"borrower_score\": 6,\n                \"weighted_score\": 0.0273\n            },\n            {\n                \"score_name\": \"ecosystem.settled_loans\",\n                \"score_value\": null,\n                \"weight\": \"25\",\n                \"maximum_score\": 10,\n                \"borrower_score\": 3,\n                \"weighted_score\": 0.0682\n            }\n        ],\n        \"total_weight\": 110,\n        \"score\": 61.12,\n        \"offers\": []\n    },\n    \"meta\": {\n        \"cost\": 15,\n        \"balance\": 1460\n    }\n}"
						}
					]
				}
			],
			"description": "These APIs provide quick, easy, and cost-effective solutions for making informed decisions during your loan decision processes, allowing you to make confident and efficient choices with ease.\n\nTo use the Decisioning APIs, you must have designed your decision models and configure them within the Lendsqr admin console."
		},
		{
			"name": "Oraculi Mobile SDK (Beta)",
			"item": [
				{
					"name": "Get User Accounts",
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "{{base_url}}oraculi/sms/entities/:bvn/accounts",
							"host": [
								"{{base_url}}oraculi"
							],
							"path": [
								"sms",
								"entities",
								":bvn",
								"accounts"
							],
							"variable": [
								{
									"key": "bvn",
									"value": null
								}
							]
						},
						"description": "This endpoint is used to get the accounts associated to a user from their bank SMS.\n\nThis API works for customers who have installed the app that has the SDK on their phones and have also granted access to the SDK to fetch their SMS data.\n\n#### Path Variables\n\n`bvn`: `required` The BVN of the user."
					},
					"response": []
				},
				{
					"name": "Get User Account Transactions",
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "{{base_url}}oraculi/sms/:phone_number/transactions",
							"host": [
								"{{base_url}}oraculi"
							],
							"path": [
								"sms",
								":phone_number",
								"transactions"
							],
							"variable": [
								{
									"key": "phone_number",
									"value": null
								}
							]
						},
						"description": "This endpoint is used to get the transactions associated to a particular bank account from the user's bank SMS.\n\n#### Path Variables\n\n`phone_number`: `required` The phone number registered on the user's bank account."
					},
					"response": []
				}
			],
			"description": "Oraculi is the Lendsqr underwriting scoring engine. Oraculi means The Oracle in Latin.\n\nLendsqr Oraculi provides a RESTful API for accessing user data gathered from your customer’s phones with the SDK you have embedded.\n\nThe SDK is only available for Android phones.",
			"event": [
				{
					"listen": "prerequest",
					"script": {
						"type": "text/javascript",
						"exec": [
							""
						]
					}
				},
				{
					"listen": "test",
					"script": {
						"type": "text/javascript",
						"exec": [
							""
						]
					}
				}
			]
		},
		{
			"name": "Embedded Loans and Payments",
			"item": [
				{
					"name": "Loans",
					"item": [
						{
							"name": "Get Loan Products",
							"request": {
								"method": "GET",
								"header": [
									{
										"key": "Authorization",
										"value": "Bearer sk_live_1wT7Xg2UxhgFUcTwhg47It14OUI18aYHbFsblcmt",
										"type": "text",
										"disabled": true
									}
								],
								"url": {
									"raw": "{{base_url}}loans/products",
									"host": [
										"{{base_url}}loans"
									],
									"path": [
										"products"
									]
								},
								"description": "This endpoint is used to retrieve all the loan products a distributor is subscribed to. As mentioned, this could be one or multiple loan product(s) from a single lender or multiple loan products from multiple lenders."
							},
							"response": [
								{
									"name": "Get Loan Products",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}loans/products",
											"host": [
												"{{base_url}}loans"
											],
											"path": [
												"products"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "77ce44b5-0e77-4b9e-98bd-cd1c29364b64"
										},
										{
											"key": "Last-Modified",
											"value": "Tue, 18 Jul 2023 07:40:31 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Content-Length",
											"value": "4427"
										},
										{
											"key": "ETag",
											"value": "W/\"114b-m9v4s05oZQ3h51ABYSfpztJ214s\""
										},
										{
											"key": "Date",
											"value": "Tue, 18 Jul 2023 07:40:34 GMT"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Keep-Alive",
											"value": "timeout=5"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"Successful\",\n    \"data\": [\n        {\n            \"product_id\": \"c9f0f895fb98ab9159f51fd0297e236d\",\n            \"name\": \"15 days for liberty\",\n            \"description\": null,\n            \"disburse_to\": \"wallet\",\n            \"collection_method\": \"debit_card\",\n            \"interest_rate\": 25,\n            \"interest_period\": null,\n            \"min_amount\": 5000,\n            \"max_amount\": 100000,\n            \"min_interest_amount\": null,\n            \"allow_multi_tenor\": 0,\n            \"frequency\": null,\n            \"min_tenor_value\": null,\n            \"min_tenor_period\": null,\n            \"max_tenor_value\": 0,\n            \"max_tenor_period\": null,\n            \"require_guarantor\": 1,\n            \"require_loan_offer\": 0\n        },\n        {\n            \"product_id\": \"45c48cce2e2d7fbdea1afc51c7c6ad26\",\n            \"name\": \"30 days for liberty\",\n            \"description\": null,\n            \"disburse_to\": \"wallet\",\n            \"collection_method\": \"debit_card\",\n            \"interest_rate\": 18,\n            \"interest_period\": null,\n            \"min_amount\": 800,\n            \"max_amount\": 9000,\n            \"min_interest_amount\": null,\n            \"allow_multi_tenor\": 0,\n            \"frequency\": null,\n            \"min_tenor_value\": null,\n            \"min_tenor_period\": null,\n            \"max_tenor_value\": 0,\n            \"max_tenor_period\": null,\n            \"require_guarantor\": 1,\n            \"require_loan_offer\": 0\n        },\n        {\n            \"product_id\": \"aab3238922bcc25a6f606eb525ffdc56\",\n            \"name\": \"Nano Loans - 15 days\",\n            \"description\": \"test\",\n            \"disburse_to\": \"wallet\",\n            \"collection_method\": \"debit_card\",\n            \"interest_rate\": 8,\n            \"interest_period\": \"months\",\n            \"min_amount\": 10,\n            \"max_amount\": 10000000,\n            \"min_interest_amount\": 9,\n            \"allow_multi_tenor\": 0,\n            \"frequency\": null,\n            \"min_tenor_value\": null,\n            \"min_tenor_period\": \"months\",\n            \"max_tenor_value\": null,\n            \"max_tenor_period\": \"months\",\n            \"require_guarantor\": 0,\n            \"require_loan_offer\": 0\n        },\n        {\n            \"product_id\": \"6f4922f45568161a8cdf4ad2299f6d23\",\n            \"name\": \"Nano Loans - 30 days\",\n            \"description\": null,\n            \"disburse_to\": \"wallet\",\n            \"collection_method\": \"debit_card\",\n            \"interest_rate\": 18,\n            \"interest_period\": null,\n            \"min_amount\": 5000,\n            \"max_amount\": 50000,\n            \"min_interest_amount\": null,\n            \"allow_multi_tenor\": 0,\n            \"frequency\": null,\n            \"min_tenor_value\": null,\n            \"min_tenor_period\": null,\n            \"max_tenor_value\": 0,\n            \"max_tenor_period\": null,\n            \"require_guarantor\": 0,\n            \"require_loan_offer\": 1\n        },\n        {\n            \"product_id\": \"ea5d2f1c4608232e07d3aa3d998e5135\",\n            \"name\": \"ussdEasy\",\n            \"description\": \"\",\n            \"disburse_to\": \"bank\",\n            \"collection_method\": \"debit_card\",\n            \"interest_rate\": 20,\n            \"interest_period\": \"flat\",\n            \"min_amount\": 1000,\n            \"max_amount\": 5000,\n            \"min_interest_amount\": 1000,\n            \"allow_multi_tenor\": 0,\n            \"frequency\": null,\n            \"min_tenor_value\": null,\n            \"min_tenor_period\": null,\n            \"max_tenor_value\": 7,\n            \"max_tenor_period\": null,\n            \"require_guarantor\": 0,\n            \"require_loan_offer\": 0\n        },\n        {\n            \"product_id\": \"fc490ca45c00b1249bbe3554a4fdf6fb\",\n            \"name\": \"ussdMedium\",\n            \"description\": \"\",\n            \"disburse_to\": \"bank\",\n            \"collection_method\": \"debit_card\",\n            \"interest_rate\": 20,\n            \"interest_period\": \"flat\",\n            \"min_amount\": 1000,\n            \"max_amount\": 5000,\n            \"min_interest_amount\": 1000,\n            \"allow_multi_tenor\": 0,\n            \"frequency\": null,\n            \"min_tenor_value\": null,\n            \"min_tenor_period\": null,\n            \"max_tenor_value\": 15,\n            \"max_tenor_period\": null,\n            \"require_guarantor\": 0,\n            \"require_loan_offer\": 0\n        },\n        {\n            \"product_id\": \"3295c76acbf4caaed33c36b1b5fc2cb1\",\n            \"name\": \"ussdHard\",\n            \"description\": \"\",\n            \"disburse_to\": \"bank\",\n            \"collection_method\": \"debit_card\",\n            \"interest_rate\": 20,\n            \"interest_period\": \"flat\",\n            \"min_amount\": 1000,\n            \"max_amount\": 5000,\n            \"min_interest_amount\": 1000,\n            \"allow_multi_tenor\": 0,\n            \"frequency\": null,\n            \"min_tenor_value\": null,\n            \"min_tenor_period\": null,\n            \"max_tenor_value\": 30,\n            \"max_tenor_period\": null,\n            \"require_guarantor\": 0,\n            \"require_loan_offer\": 0\n        },\n        {\n            \"product_id\": \"a597e50502f5ff68e3e25b9114205d4a\",\n            \"name\": \"30 days for liberty\",\n            \"description\": null,\n            \"disburse_to\": \"wallet\",\n            \"collection_method\": \"debit_card\",\n            \"interest_rate\": 10,\n            \"interest_period\": \"months\",\n            \"min_amount\": 1000,\n            \"max_amount\": 9000,\n            \"min_interest_amount\": 1000,\n            \"allow_multi_tenor\": 1,\n            \"frequency\": null,\n            \"min_tenor_value\": 1,\n            \"min_tenor_period\": \"months\",\n            \"max_tenor_value\": 5,\n            \"max_tenor_period\": \"months\",\n            \"require_guarantor\": 1,\n            \"require_loan_offer\": 0\n        },\n        {\n            \"product_id\": \"0336dcbab05b9d5ad24f4333c7658a0e\",\n            \"name\": \"30 days for liberty\",\n            \"description\": null,\n            \"disburse_to\": \"wallet\",\n            \"collection_method\": \"debit_card\",\n            \"interest_rate\": 10,\n            \"interest_period\": \"months\",\n            \"min_amount\": 3000,\n            \"max_amount\": 9000,\n            \"min_interest_amount\": 1000,\n            \"allow_multi_tenor\": 1,\n            \"frequency\": null,\n            \"min_tenor_value\": 15,\n            \"min_tenor_period\": \"days\",\n            \"max_tenor_value\": 90,\n            \"max_tenor_period\": \"days\",\n            \"require_guarantor\": 1,\n            \"require_loan_offer\": 0\n        },\n        {\n            \"product_id\": \"34ed066df378efacc9b924ec161e7639\",\n            \"name\": \"LC Multi tenor test\",\n            \"description\": \"Test for LC Multi tenor\",\n            \"disburse_to\": \"wallet\",\n            \"collection_method\": \"debit_card\",\n            \"interest_rate\": 5,\n            \"interest_period\": \"months\",\n            \"min_amount\": 5000,\n            \"max_amount\": 50000,\n            \"min_interest_amount\": 1000,\n            \"allow_multi_tenor\": 1,\n            \"frequency\": \"monthly\",\n            \"min_tenor_value\": 1,\n            \"min_tenor_period\": \"months\",\n            \"max_tenor_value\": 3,\n            \"max_tenor_period\": \"months\",\n            \"require_guarantor\": 0,\n            \"require_loan_offer\": 0\n        }\n    ]\n}"
								}
							]
						},
						{
							"name": "Initialize Loan Application",
							"request": {
								"method": "POST",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"product_id\": \"c9f0f895fb98ab9159f51fd0297e236d\",\n    \"meta\": {\n        \"email\": \"froggy@lendsqr.com\",\n        \"phone_number\": \"08089722636\"\n    }\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}loans/initialize",
									"host": [
										"{{base_url}}loans"
									],
									"path": [
										"initialize"
									]
								},
								"description": "Using the product ID that has been retrieved from the GET loan products endpoint, make a call to this endpoint to generate the web page URL that can be embedded within your web or mobile platform.\n\nThe request body also allows for meta fields that would prepoulate and disable these form fields within the the web page\n\n> NOTE: All fields on the web page would be disabled except email and phone number as these details may be different on the lender's plaform. \n  \n\n### Meta fields\n| Property | Type | Details | **Options** |\n| --- | --- | --- | --- |\n| `requested_amount` | number | This should be the amount the customer wants to check out with (BNPL) or has requested.  <br>Currency is in Naira | NA |\n| `proposed_tenor` | number | This is the duration for the loan before repayment kicks in. The range for this is decided by the loan product selected however customers can specify any value within that range. | NA |\n| `proposed_tenor_period` | `string` | This is the measurement of time that drives the proposed_tenor entered | days  <br>weeks  <br>months |\n| `gender` | `string` | male, female | male;  <br>female |\n| `marital_status` | `string` | The marital status of the user | married;  <br>single;  <br>divorced;  <br>separated;  <br>widowed |\n| `location` | `string` | The residential state of the user | States only:  <br>Lagos;  <br>Oyo etc. |\n| `no_of_dependent` | integer | 0, 5 | 0,  <br>5 etc. |\n| `type_of_residence` | `string` | The type of home residence the user lives in. There are currently three options | own house,  <br>rented apartment, parents apartment |\n| `education_attainment` | `string` | The highest level of eductaional attainment by the user. There are currently four options | MSc and above;  <br>BSc, HND and Other Equivalent;  <br>Diploma/School Cert; Others |\n| `employment_status` | `string` | The employment status of the user. There are currently four options | employed,  <br>self employed, unemployed,  <br>retired |\n| `bvn` | `string` | 22222222222 | NA |\n| `phone_number` | `string` | 0805555555 |  |\n| `working_period` | integer | 1 |  |\n| `time_with_current_employer` | integer | 1 |  |\n| `bvn_phone` | `string` | 08106666666 |  |\n| `official_email` | `string` | [male@female.com](https://) |  |\n| `personal_email` | `string` | [male@female.com](https://) |  |\n| `amount` | `string` | 5000 |  |"
							},
							"response": [
								{
									"name": "Initialize Loan Application",
									"originalRequest": {
										"method": "POST",
										"header": [],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"product_id\": \"c9f0f895fb98ab9159f51fd0297e236d\",\n    \"meta\": {\n        \"email\": \"ado.john.sule@example.com\",\n        \"phone_number\": \"08012345678\"\n    }\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{base_url}}loans/initialize",
											"host": [
												"{{base_url}}loans"
											],
											"path": [
												"initialize"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "b3702fe8-c53f-49dc-b708-b0cf1b237184"
										},
										{
											"key": "Last-Modified",
											"value": "Tue, 18 Jul 2023 08:05:17 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Content-Length",
											"value": "81"
										},
										{
											"key": "ETag",
											"value": "W/\"51-OSar/GFq53hdcXnYSHcSuWvsar4\""
										},
										{
											"key": "Date",
											"value": "Tue, 18 Jul 2023 08:05:24 GMT"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Keep-Alive",
											"value": "timeout=5"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"Successful\",\n    \"data\": {\n        \"reference\": \"LSQDTmKBFL04sO2F29Fl\",\n        \"url\": \"https://l.lsq.li/2Yg\"\n    }\n}"
								}
							]
						},
						{
							"name": "Get Loan",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}loans/:reference",
									"host": [
										"{{base_url}}loans"
									],
									"path": [
										":reference"
									],
									"variable": [
										{
											"key": "reference",
											"value": "LSQDTCdGYL0ktgJnO0bs"
										}
									]
								},
								"description": "This endpoint is used to retrieve the details of a loan or loan request made via your platform as a distributor."
							},
							"response": [
								{
									"name": "Get Loan",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}loans/:reference",
											"host": [
												"{{base_url}}loans"
											],
											"path": [
												":reference"
											],
											"variable": [
												{
													"key": "reference",
													"value": "LSQDTCdGYL0ktgJnO0bs"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "1016848a-b496-49c5-84d3-a920397d22dc"
										},
										{
											"key": "Last-Modified",
											"value": "Thu, 20 Jul 2023 08:29:09 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Content-Length",
											"value": "742"
										},
										{
											"key": "ETag",
											"value": "W/\"2e6-CTC54l/r/cxZ3rlqhKA+gFUyZyk\""
										},
										{
											"key": "Date",
											"value": "Thu, 20 Jul 2023 08:29:13 GMT"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Keep-Alive",
											"value": "timeout=5"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"Successful\",\n    \"data\": {\n        \"customer_type\": \"Individual\",\n        \"tenor\": 6,\n        \"tenor_period\": \"weeks\",\n        \"status\": {\n            \"status\": \"CANCELLED\",\n            \"can_request\": 1,\n            \"can_cancel\": 0\n        },\n        \"user\": {\n            \"first_name\": \"Ado\",\n            \"last_name\": \"John Sule\",\n            \"phone_number\": \"08012345678\",\n            \"email\": \"\",\n            \"photo_url\": \"https://picsum.photos/id/1/5000/3333\",\n            \"referral_code\": \"FUER4D\"\n        },\n        \"interest_rate\": 5,\n        \"interest_period\": \"months\",\n        \"reference\": \"LSQDTCdGYL0ktgJnO0bs\",\n        \"loan_amount\": 5000,\n        \"interest_due\": 1000,\n        \"amount_disbursed\": null,\n        \"paid\": 0,\n        \"reject_reason\": null,\n        \"channel\": \"web\",\n        \"disburse_to\": \"wallet\",\n        \"multi_tenor\": false,\n        \"payment_link_hash\": \"blej\"\n    }\n}"
								}
							]
						}
					],
					"description": "Embedded loans allows you as a third-party to offer loan services to your customers on your platform without having to be a lender yourself.",
					"event": [
						{
							"listen": "prerequest",
							"script": {
								"type": "text/javascript",
								"exec": [
									""
								]
							}
						},
						{
							"listen": "test",
							"script": {
								"type": "text/javascript",
								"exec": [
									""
								]
							}
						}
					]
				},
				{
					"name": "Pay with wallet",
					"item": [
						{
							"name": "Initialize Payment",
							"request": {
								"method": "POST",
								"header": [
									{
										"key": "Authorization",
										"value": "Bearer sk_test_5N5FcApMCqN0DsDH3r6Ve292Q2peJGC2ZIynMab0",
										"type": "text"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"amount\": 5000,\n    \"description\": \"Payment for beans, yam and egg\",\n    \"organization_id\": \"37a749d808e46495a8da1e5352d03cae\",\n    \"callback_url\": \"https://lendsqr.com\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}payments/initialize",
									"host": [
										"{{base_url}}payments"
									],
									"path": [
										"initialize"
									]
								},
								"description": "This endpoint generates the payment link that would open a web page that would allow customers to log into the lender's account and initiate the relevant payment.\n\nYou would provide us with a callback URL that would serve as a redirect for customers once payment has been made."
							},
							"response": [
								{
									"name": "Initialize Payment",
									"originalRequest": {
										"method": "POST",
										"header": [
											{
												"key": "Authorization",
												"value": "Bearer sk_test_5N5FcApMCqN0DsDH3r6Ve292Q2peJGC2ZIynMab0",
												"type": "text"
											}
										],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"amount\": 5000,\n    \"description\": \"Payment for beans and egg\"\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{base_url}}payments/initialize",
											"host": [
												"{{base_url}}payments"
											],
											"path": [
												"initialize"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "b90557c9-1497-414f-86b4-9f89d3361e52"
										},
										{
											"key": "Last-Modified",
											"value": "Sun, 23 Jul 2023 18:55:19 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Content-Length",
											"value": "108"
										},
										{
											"key": "ETag",
											"value": "W/\"6c-IGmND8VHD+WKmPUjHpwPnBLnwk8\""
										},
										{
											"key": "Date",
											"value": "Sun, 23 Jul 2023 18:55:20 GMT"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Keep-Alive",
											"value": "timeout=5"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"Successful\",\n    \"data\": {\n        \"reference\": \"9ZyuoKwn3ENs12YU\",\n        \"url\": \"9ZyuoKwn3ENs12YU\"\n    }\n}"
								}
							]
						},
						{
							"name": "Query Payment",
							"request": {
								"method": "GET",
								"header": [
									{
										"key": "Authorization",
										"value": "Bearer sk_test_5N5FcApMCqN0DsDH3r6Ve292Q2peJGC2ZIynMab0",
										"type": "text",
										"disabled": true
									}
								],
								"url": {
									"raw": "{{base_url}}payments/:reference",
									"host": [
										"{{base_url}}payments"
									],
									"path": [
										":reference"
									],
									"variable": [
										{
											"key": "reference",
											"value": ""
										}
									]
								},
								"description": "This endpoint is used to query the details of the payment made."
							},
							"response": [
								{
									"name": "Query Payment",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "Authorization",
												"value": "Bearer sk_test_5N5FcApMCqN0DsDH3r6Ve292Q2peJGC2ZIynMab0",
												"type": "text"
											}
										],
										"url": {
											"raw": "{{base_url}}payments/9ZyuoKwn3ENs12YU",
											"host": [
												"{{base_url}}payments"
											],
											"path": [
												"9ZyuoKwn3ENs12YU"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "43840982-dee5-49a3-acda-4650c01a11cf"
										},
										{
											"key": "Last-Modified",
											"value": "Sun, 23 Jul 2023 18:56:43 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Content-Length",
											"value": "369"
										},
										{
											"key": "ETag",
											"value": "W/\"171-zzSQFFLrRm98A9YAgrI4FQiBWHs\""
										},
										{
											"key": "Date",
											"value": "Sun, 23 Jul 2023 18:56:44 GMT"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Keep-Alive",
											"value": "timeout=5"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"Successful\",\n    \"data\": {\n        \"id\": 3,\n        \"org_id\": 136,\n        \"distributor_id\": 2,\n        \"transaction_id\": null,\n        \"reference\": \"9ZyuoKwn3ENs12YU\",\n        \"amount\": 5000,\n        \"description\": \"Payment for beans and egg\",\n        \"callback_url\": null,\n        \"created_on\": \"2023-07-23T17:55:20.000Z\",\n        \"created_by\": null,\n        \"modified_on\": null,\n        \"modified_by\": null,\n        \"deleted_flag\": 0,\n        \"deleted_on\": null,\n        \"deleted_by\": null\n    }\n}"
								}
							]
						}
					],
					"description": "Our Pay with Wallet solution allows your customers to make payment for their purchases via various account holding platforms. This solution is viable to customers who have accounts with a lender, on the Lendsqr platform that is activated for this program."
				}
			],
			"description": "## Introduction\n\nEmbedded loans and payments offers third-party distributors with Lendsqr the option to offer loans and payment options to customers on their platform outside Lendsqr."
		},
		{
			"name": "Data for Lenders",
			"item": [
				{
					"name": "Options",
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "{{base_url}}data/options",
							"host": [
								"{{base_url}}data"
							],
							"path": [
								"options"
							]
						},
						"description": "This endpoint is used to get the data options or sources available for a lender.\n\n#### Response Payload\n\n| Field | Type | Description |\n| --- | --- | --- |\n| name | `string` | \"Users\" |\n| description | `string` | \"Get details of all users that have signed up to the system. This may include users who have not completed their onboarding\" |\n| path | `string` | \"/users\" |"
					},
					"response": [
						{
							"name": "Data Options",
							"originalRequest": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}data/options",
									"host": [
										"{{base_url}}data"
									],
									"path": [
										"options"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Wed, 28 Feb 2024 22:55:02 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json; charset=utf-8"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "X-Powered-By",
									"value": "Express"
								},
								{
									"key": "X-Request-ID",
									"value": "286bceb2-43a0-4cc6-a001-131f13a66e3c"
								},
								{
									"key": "Last-Modified",
									"value": "Wed, 28 Feb 2024 22:54:57 GMT"
								},
								{
									"key": "ETag",
									"value": "W/\"690-sCrGprb2Do2p61q0+9QpVPX9kU8\""
								},
								{
									"key": "CF-Cache-Status",
									"value": "DYNAMIC"
								},
								{
									"key": "Server",
									"value": "cloudflare"
								},
								{
									"key": "CF-RAY",
									"value": "85cc40948afa636a-LHR"
								},
								{
									"key": "Content-Encoding",
									"value": "gzip"
								}
							],
							"cookie": [],
							"body": "{\n    \"success\": true,\n    \"data\": [\n        {\n            \"name\": \"Users\",\n            \"description\": \"Get details of all users that have signed up to the system. This may include users who have not completed their onboarding\",\n            \"path\": \"/users\"\n        },\n        {\n            \"name\": \"Loans\",\n            \"description\": \"Get details of all loans for any users. You can filter with user_id, status, and approved_on columns\",\n            \"path\": \"/loans\"\n        },\n        {\n            \"name\": \"Options\",\n            \"description\": \"List all available data options. To get the data for any path, please call with base_url/<path>\",\n            \"path\": \"/options\"\n        },\n        {\n            \"name\": \"Lenders\",\n            \"description\": \"Get the list of all the lenders within the system. Should not appear for anyone\",\n            \"path\": \"/lenders\"\n        },\n        {\n            \"name\": \"Loan analytics\",\n            \"description\": \"Analytics of loans for organization grouped by month. You can filter with the month column\",\n            \"path\": \"/analytics/loans\"\n        },\n        {\n            \"name\": \"Loans\",\n            \"description\": \"Get transactions for loans. You can filter data using the loan_id and created_on columns\",\n            \"path\": \"/loans/transactions\"\n        },\n        {\n            \"name\": \"Loans\",\n            \"description\": \"Get schedules for specific loans. You can filter data using the loan_id and created_on columns\",\n            \"path\": \"/loans/schedules\"\n        },\n        {\n            \"name\": \"Transactions\",\n            \"description\": \"Get details of all user transactions. You can filter data using the user_id column\",\n            \"path\": \"/transactions\"\n        },\n        {\n            \"name\": \"Top offers\",\n            \"description\": \"Get the list of top loan offers in the Lendsqr ecosystem.\",\n            \"path\": \"/lenders/top-offers\"\n        },\n        {\n            \"name\": \"Lenders loans\",\n            \"description\": \"Get the list of all the loans that all lenders in the Lendsqr ecosystem have\",\n            \"path\": \"/lenders/loans\"\n        },\n        {\n            \"name\": \"Cards\",\n            \"description\": \"Get details of all cards.\",\n            \"path\": \"/cards\"\n        },\n        {\n            \"name\": \"Bank Accounts\",\n            \"description\": \"Get details of all bank accounts.\",\n            \"path\": \"/bank-accounts\"\n        }\n    ]\n}"
						}
					]
				},
				{
					"name": "Users",
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "{{base_url}}data/users",
							"host": [
								"{{base_url}}data"
							],
							"path": [
								"users"
							]
						},
						"description": "| Field | Type | Description |\n| --- | --- | --- |\n| org_id | `integer` | 9999 |\n| organization | `string` | \"Example Lender\" |\n| id | `integer` | 44691 |\n| first_name | `string` | \"Ado\\`\" |\n| last_name | `string` | \"John Sule\" |\n| full_name | `string` | \"Ado John Sule\" |\n| phone_number | `string` | \"07062569817\" |\n| phone_number_hash | `string` | \"318c88a8e1fcfc049114e69128275b4d\" |\n| email | `string` | \"Ado@lendsqr.com\" |\n| bvn | `string` | \"21234567890\" |\n| bvn_phone_number | `string` | \"08012345678\" |\n| `date`_of_birth | `date` | \"1990-09-10\" |\n| age | `integer` | 26 |\n| gender | `string` | \"Female\" |\n| stage_id | `integer` | 6 |\n| stage | `string` | \"done\" |\n| photo_url | `string` | \"[https://image.url.com\"](https://image.url.com) |\n| mifos_client_id | `string` | \"41053\" |\n| client_id | `string` | \"41053\" |\n| savings_id | `string` | \"47197\" |\n| account_number | `string` | \"IDR000047197----------\" |\n| account_balance | `float` | 1144.25 |\n| account_name | `string` | \"Ado John Sule\" |\n| referral_code | `string` | \"B7YEHI\" |\n| device_id | `string` | \"bd96e5e050c0529d\" |\n| notification_token | `string` | \"****\" |\n| device_type | `string` | \"Android\" |\n| tier_id | `integer` | 24 |\n| tier | `string` | \"Tier 3\" |\n| withdrawal_limit | `integer` | 1000000 |\n| deposit_limit | `integer` | 20000 |\n| borrower_max_cumulative_amount | `float` | 999999999999 |\n| support_email | `string` | \"support@example.com\" |\n| loan_count | `integer` | 14 |\n| savings_plans | `integer` | 0 |\n| savings_target | `integer` | 0 |\n| savings_balance | `integer` | 0 |\n| activated | `integer` | 1 |\n| activated_on | `datetime` |  |\n| blacklisted | `integer` | 0 |\n| reason | `string` | null |\n| selfie_bvn_check | `string` | \"Successful\" |\n| selfie_id_check | `string` | \"Successful\" |\n| nok_first_name | `string` | \"Evelyn\" |\n| nok_last_name | `string` | \"Peters\" |\n| nok_phone_number | `string` | \"09099494342\" |\n| nok_email | `string` | \"evelyn@lendsqr.com\" |\n| nok_address | `string` | \"Ayodele Oke-Owo Street Gbagada\" |\n| nok_relationship | `string` | \"Others\" |\n| marital_status | `string` | \"Single\" |\n| no_of_dependent | `string` | \"0\" |\n| type_of_residence | `string` | \"Parents Apartment\" |\n| educational_attainment | `string` | \"BSc, HND and Other Equivalent\" |\n| employment_status | `string` | \"Employed\" |\n| sector_of_employment | `string` | \"Other Financial\" |\n| current_employer | `string` | \"Lendsqr\" |\n| employment_category | `string` | \"Private Company\" |\n| monthly_net_income | `string` | \"200,000 - 399,999\" |\n| work_start_date | `datetime` |  |\n| work_email | `string` | \"ado@example.com\" |\n| country | `string` | \"NGA\" |\n| city | `string` | \"Gbagada\" |\n| lga | `string` | \"Kosofe\" |\n| street | null | null |\n| nearest_landmark | `string` | \"Deeper Life Church\" |\n| longitude | `float` | \\-102.0837554932 |\n| latitude | `float` | 47.421546936 |\n| address | `string` | \"Lagos\" |"
					},
					"response": [
						{
							"name": "Users",
							"originalRequest": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}data/users",
									"host": [
										"{{base_url}}data"
									],
									"path": [
										"users"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "Date",
									"value": "Wed, 28 Feb 2024 23:05:31 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json; charset=utf-8"
								},
								{
									"key": "Transfer-Encoding",
									"value": "chunked"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "X-Powered-By",
									"value": "Express"
								},
								{
									"key": "X-Request-ID",
									"value": "2b47c2f1-dea7-4c19-8250-e05e43f48ed0"
								},
								{
									"key": "Last-Modified",
									"value": "Wed, 28 Feb 2024 23:05:29 GMT"
								},
								{
									"key": "ETag",
									"value": "W/\"39515-/Q53k0DdvDTRus/qCQzKY2+97vM\""
								},
								{
									"key": "CF-Cache-Status",
									"value": "DYNAMIC"
								},
								{
									"key": "Server",
									"value": "cloudflare"
								},
								{
									"key": "CF-RAY",
									"value": "85cc5004cf47636a-LHR"
								},
								{
									"key": "Content-Encoding",
									"value": "gzip"
								}
							],
							"cookie": [],
							"body": "{\n    \"success\": true,\n    \"data\": [\n        {\n            \"org_id\": 9999,\n            \"organization\": \"Example Lender\",\n            \"id\": 44691,\n            \"first_name\": \"Ado`\",\n            \"last_name\": \"John Sule\",\n            \"full_name\": \"Ado John Sule\",\n            \"phone_number\": \"07062569817\",\n            \"phone_number_hash\": \"318c88a8e1fcfc049114e69128275b4d\",\n            \"email\": \"Ado@lendsqr.com\",\n            \"bvn\": \"21234567890\",\n            \"bvn_phone_number\": \"08012345678\",\n            \"date_of_birth\": \"1990-09-10\",\n            \"age\": 26,\n            \"gender\": \"Female\",\n            \"stage_id\": 6,\n            \"stage\": \"done\",\n            \"photo_url\": \"https://image.url.com\",\n            \"mifos_client_id\": \"41053\",\n            \"client_id\": \"41053\",\n            \"savings_id\": \"47197\",\n            \"account_number\": \"IDR000047197----------\",\n            \"account_balance\": 1144.25,\n            \"account_name\": \"Ado John Sule\",\n            \"referral_code\": \"B7YEHI\",\n            \"referred_by\": null,\n            \"referrer_name\": null,\n            \"referrer_email\": null,\n            \"referrer_phone\": null,\n            \"referrer_code\": null,\n            \"device_id\": \"bd96e5e050c0529d\",\n            \"notification_token\": \"********************************\",\n            \"device_type\": \"Android\",\n            \"tier_id\": 24,\n            \"tier\": \"Tier 3\",\n            \"withdrawal_limit\": 1000000,\n            \"deposit_limit\": 20000,\n            \"borrower_max_cumulative_amount\": 999999999999,\n            \"support_email\": \"support@example.com\",\n            \"loan_count\": 14,\n            \"savings_plans\": 0,\n            \"savings_target\": 0,\n            \"savings_balance\": 0,\n            \"activated\": 1,\n            \"activated_on\": \"2021-02-01T10:15:08.000Z\",\n            \"blacklisted\": 0,\n            \"reason\": null,\n            \"selfie_bvn_check\": \"Successful\",\n            \"selfie_id_check\": \"Successful\",\n            \"last_login_date\": \"2023-10-02T23:20:36.000Z\",\n            \"created_on\": \"2021-02-01T11:02:00.000Z\",\n            \"modified_on\": \"2023-10-02T23:20:36.000Z\",\n            \"deleted_on\": null,\n            \"nok_first_name\": \"Evelyn\",\n            \"nok_last_name\": \"Peters\",\n            \"nok_phone_number\": \"09099494342\",\n            \"nok_email\": \"evelyn@lendsqr.com\",\n            \"nok_address\": \"Ayodele Oke-Owo Street  Gbagada\",\n            \"nok_relationship\": \"Others\",\n            \"marital_status\": \"Single\",\n            \"no_of_dependent\": \"0\",\n            \"type_of_residence\": \"Parents Apartment\",\n            \"educational_attainment\": \"BSc, HND and Other Equivalent\",\n            \"employment_status\": \"Employed\",\n            \"sector_of_employment\": \"Other Financial\",\n            \"current_employer\": \"Lendsqr\",\n            \"employment_category\": \"Private Company\",\n            \"monthly_net_income\": \"200,000 - 399,999\",\n            \"work_start_date\": \"2020-11-15T23:00:00.000Z\",\n            \"work_email\": \"ado@example.com\",\n            \"country\": \"NGA\",\n            \"city\": \"Gbagada\",\n            \"lga\": \"Kosofe\",\n            \"street\": null,\n            \"nearest_landmark\": \"Deeper Life Church\",\n            \"longitude\": -102.0837554932,\n            \"latitude\": 47.421546936,\n            \"address\": \"Lagos\",\n            \"process_time\": \"2024-02-28T03:20:26.000Z\"\n        }\n    ]\n}"
						}
					]
				}
			],
			"description": "### Introduction\n\nLenders and their customers generate a lot of data that are important for lenders outside of the Lendsqr ecosystem. Lendsqr allows lenders to use Adjutor APIs to get these data. There are almost infinite limits to the data a lender can get for their customers, transactions, audit activities, etc."
		},
		{
			"name": "Operational Services",
			"item": [
				{
					"name": "Profile",
					"item": [
						{
							"name": "Get Adjutor Services Pricing",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}profile/pricing",
									"host": [
										"{{base_url}}profile"
									],
									"path": [
										"pricing"
									]
								},
								"description": "This endpoint is used to obtain the current pricing of the API services. Kindly note that pricing may be different from lender to lender due to commercial negotiations that could have provide some lenders with a different pricing due to volume commitment.\n\nIf you want a cheaper price, which usually comes with a minimum monthly spend, please contact your account manager at growth@lendsqr.com."
							},
							"response": [
								{
									"name": "Get Adjutor Services Pricing",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}profile/pricing",
											"host": [
												"{{base_url}}profile"
											],
											"path": [
												"pricing"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Mon, 14 Aug 2023 13:29:17 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "ffce023d-0a92-4484-ac47-7923b86002b5"
										},
										{
											"key": "Last-Modified",
											"value": "Mon, 14 Aug 2023 13:29:16 GMT"
										},
										{
											"key": "ETag",
											"value": "W/\"2bc-wuQroduQ50LikXzniRq/QTN48cQ\""
										},
										{
											"key": "CF-Cache-Status",
											"value": "DYNAMIC"
										},
										{
											"key": "Server",
											"value": "cloudflare"
										},
										{
											"key": "CF-RAY",
											"value": "7f698bb35ab303d6-LIS"
										},
										{
											"key": "Content-Encoding",
											"value": "gzip"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"Successful\",\n    \"data\": [\n        {\n            \"name\": \"Adjutor Oraculi Scoring\",\n            \"amount\": 15\n        },\n        {\n            \"name\": \"Adjutor Name Inquiry\",\n            \"amount\": 0\n        },\n        {\n            \"name\": \"Adjutor Name Inquiry with BVN\",\n            \"amount\": 10\n        },\n        {\n            \"name\": \"Adjutor Karma Lookup\",\n            \"amount\": 10\n        },\n        {\n            \"name\": \"Adjutor BVN Verification\",\n            \"amount\": 20\n        },\n        {\n            \"name\": \"Adjutor Image Compare\",\n            \"amount\": 30\n        },\n        {\n            \"name\": \"Adjutor Ecosystem Lookup\",\n            \"amount\": 25\n        },\n        {\n            \"name\": \"Adjutor Bank List\",\n            \"amount\": 0\n        },\n        {\n            \"name\": \"Adjutor CRC\",\n            \"amount\": 100\n        },\n        {\n            \"name\": \"Adjutor Oraculi Central\",\n            \"amount\": 100\n        },\n        {\n            \"name\": \"Adjutor Credit Registry\",\n            \"amount\": 1500\n        },\n        {\n            \"name\": \"Adjutor Oraculi Accounts\",\n            \"amount\": 10\n        },\n        {\n            \"name\": \"Adjutor Oraculi Statements\",\n            \"amount\": 25\n        },\n        {\n            \"name\": \"Adjutor Oraculi Analytics\",\n            \"amount\": 25\n        }\n    ]\n}"
								}
							]
						},
						{
							"name": "Get Wallet",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}profile/wallet",
									"host": [
										"{{base_url}}profile"
									],
									"path": [
										"wallet"
									]
								},
								"description": "This request is used to obtain the wallet information on the lender's profile."
							},
							"response": []
						},
						{
							"name": "Get API Audit Logs",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}profile/audit?page=1&limit=20",
									"host": [
										"{{base_url}}profile"
									],
									"path": [
										"audit"
									],
									"query": [
										{
											"key": "page",
											"value": "1"
										},
										{
											"key": "limit",
											"value": "20"
										}
									]
								},
								"description": "This endpoint is used to get the audit logs of the API calls made on the profile.\n\n`This endpoint is currently under development`"
							},
							"response": []
						}
					]
				},
				{
					"name": "Miscellaneous",
					"item": [
						{
							"name": "Get List of Banks",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}banks",
									"host": [
										"{{base_url}}banks"
									]
								},
								"description": "This endpoint is used for getting banks and their codes.\n\n#### Response Code\n\n| Field | Type | Description |\n| --- | --- | --- |\n| name | `string` | The name of the bank (e.g., \"Access Bank\"). |\n| shortcode | `string` | A unique code for the bank issued by the Central Bank of Nigeria (e.g., \"044\"). |\n| longcode | `string` | A unique code for the bank on the NIBSS network (e.g., \"000014\"). |"
							},
							"response": [
								{
									"name": "Get List of Banks",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}banks",
											"host": [
												"{{base_url}}banks"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Mon, 14 Aug 2023 13:17:55 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "1c82274f-e038-4de1-998d-8d16b721d3c5"
										},
										{
											"key": "Last-Modified",
											"value": "Mon, 14 Aug 2023 13:17:53 GMT"
										},
										{
											"key": "ETag",
											"value": "W/\"dcc-ImNirDzX8D8qoFcwASXEATbzskg\""
										},
										{
											"key": "CF-Cache-Status",
											"value": "DYNAMIC"
										},
										{
											"key": "Server",
											"value": "cloudflare"
										},
										{
											"key": "CF-RAY",
											"value": "7f697b067a3ed42c-LOS"
										},
										{
											"key": "Content-Encoding",
											"value": "gzip"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"Successful\",\n    \"data\": [\n        {\n            \"name\": \"3line\",\n            \"shortcode\": null,\n            \"longcode\": \"110005\"\n        },\n        {\n            \"name\": \"Access Bank\",\n            \"shortcode\": \"044\",\n            \"longcode\": \"000014\"\n        },\n        {\n            \"name\": \"Alat by Wema\",\n            \"shortcode\": \"035\",\n            \"longcode\": \"000017\"\n        },\n        {\n            \"name\": \"ASO Savings and Loans\",\n            \"shortcode\": \"401\",\n            \"longcode\": \"090001\"\n        },\n        {\n            \"name\": \"Bankly MBF\",\n            \"shortcode\": \"\",\n            \"longcode\": \"090529\"\n        },\n        {\n            \"name\": \"Carbon\",\n            \"shortcode\": \"565\",\n            \"longcode\": \"100026\"\n        },\n        {\n            \"name\": \"CEMCS Microfinance Bank\",\n            \"shortcode\": \"50823\",\n            \"longcode\": \"090154\"\n        },\n        {\n            \"name\": \"Citibank Nigeria\",\n            \"shortcode\": \"023\",\n            \"longcode\": \"000009\"\n        },\n        {\n            \"name\": \"Conpro MFB (Kredi Bank)\",\n            \"shortcode\": \"50200\",\n            \"longcode\": \"090380\"\n        },\n        {\n            \"name\": \"Coronation Merchant Bank\",\n            \"shortcode\": \"559\",\n            \"longcode\": \"060001\"\n        },\n        {\n            \"name\": \"Dot pay\",\n            \"shortcode\": null,\n            \"longcode\": \"090470\"\n        },\n        {\n            \"name\": \"Ecobank Nigeria\",\n            \"shortcode\": \"050\",\n            \"longcode\": \"000010\"\n        },\n        {\n            \"name\": \"Ekondo Microfinance Bank\",\n            \"shortcode\": \"562\",\n            \"longcode\": \"090097\"\n        },\n        {\n            \"name\": \"Fairmoney MFB\",\n            \"shortcode\": \"\",\n            \"longcode\": \"090551\"\n        },\n        {\n            \"name\": \"FBNQuest Merchant Bank\",\n            \"shortcode\": \"911\",\n            \"longcode\": \"060002\"\n        },\n        {\n            \"name\": \"Fidelity Bank\",\n            \"shortcode\": \"070\",\n            \"longcode\": \"000007\"\n        },\n        {\n            \"name\": \"Firmus MFB\",\n            \"shortcode\": \"51314\",\n            \"longcode\": \"090366\"\n        },\n        {\n            \"name\": \"First Bank of Nigeria\",\n            \"shortcode\": \"011\",\n            \"longcode\": \"000016\"\n        },\n        {\n            \"name\": \"First City Monument Bank\",\n            \"shortcode\": \"214\",\n            \"longcode\": \"000003\"\n        },\n        {\n            \"name\": \"FSDH Merchant Bank\",\n            \"shortcode\": \"501\",\n            \"longcode\": \"400001\"\n        },\n        {\n            \"name\": \"Globus Bank\",\n            \"shortcode\": \"103\",\n            \"longcode\": \"000027\"\n        },\n        {\n            \"name\": \"Guaranty Trust Bank\",\n            \"shortcode\": \"058\",\n            \"longcode\": \"000013\"\n        },\n        {\n            \"name\": \"Hasal Microfinance Bank\",\n            \"shortcode\": \"50383\",\n            \"longcode\": \"090121\"\n        },\n        {\n            \"name\": \"Heritage Bank\",\n            \"shortcode\": \"030\",\n            \"longcode\": \"000020\"\n        },\n        {\n            \"name\": \"Jaiz Bank\",\n            \"shortcode\": \"301\",\n            \"longcode\": \"000006\"\n        },\n        {\n            \"name\": \"Keystone Bank\",\n            \"shortcode\": \"082\",\n            \"longcode\": \"000002\"\n        },\n        {\n            \"name\": \"Kuda Bank\",\n            \"shortcode\": \"50211\",\n            \"longcode\": \"090267\"\n        },\n        {\n            \"name\": \"MoniePoint Bank\",\n            \"shortcode\": \"50515\",\n            \"longcode\": \"090405\"\n        },\n        {\n            \"name\": \"Nova Merchant Bank\",\n            \"shortcode\": \"561\",\n            \"longcode\": \"060003\"\n        },\n        {\n            \"name\": \"Nuntius Internal Bank\",\n            \"shortcode\": \"999999\",\n            \"longcode\": \"999999\"\n        },\n        {\n            \"name\": \"One Finance\",\n            \"shortcode\": \"565\",\n            \"longcode\": \"100026\"\n        },\n        {\n            \"name\": \"Palmpay\",\n            \"shortcode\": \"100033\",\n            \"longcode\": \"100033\"\n        },\n        {\n            \"name\": \"Parallex Bank\",\n            \"shortcode\": \"526\",\n            \"longcode\": \"090004\"\n        },\n        {\n            \"name\": \"paycom (Opay)\",\n            \"shortcode\": \"305\",\n            \"longcode\": \"100004\"\n        },\n        {\n            \"name\": \"Polaris Bank\",\n            \"shortcode\": \"076\",\n            \"longcode\": \"000008\"\n        },\n        {\n            \"name\": \"Providus Bank\",\n            \"shortcode\": \"101\",\n            \"longcode\": \"000023\"\n        },\n        {\n            \"name\": \"Rand Merchant Bank Nigeria\",\n            \"shortcode\": \"502\",\n            \"longcode\": \"000024\"\n        },\n        {\n            \"name\": \"Rubies MFB\",\n            \"shortcode\": \"125\",\n            \"longcode\": \"090175\"\n        },\n        {\n            \"name\": \"Sparkle Microfinance Bank\",\n            \"shortcode\": \"51310\",\n            \"longcode\": \"090325\"\n        },\n        {\n            \"name\": \"Stanbic IBTC Bank\",\n            \"shortcode\": \"221\",\n            \"longcode\": \"000012\"\n        },\n        {\n            \"name\": \"Standard Chartered Bank\",\n            \"shortcode\": \"068\",\n            \"longcode\": \"000021\"\n        },\n        {\n            \"name\": \"Sterling Bank\",\n            \"shortcode\": \"232\",\n            \"longcode\": \"000001\"\n        },\n        {\n            \"name\": \"Suntrust Bank\",\n            \"shortcode\": \"100\",\n            \"longcode\": \"000022\"\n        },\n        {\n            \"name\": \"Support MFB\",\n            \"shortcode\": \"295\",\n            \"longcode\": \"090446\"\n        },\n        {\n            \"name\": \"TAJ Bank\",\n            \"shortcode\": \"302\",\n            \"longcode\": \"000026\"\n        },\n        {\n            \"name\": \"TCF MFB\",\n            \"shortcode\": \"51211\",\n            \"longcode\": \"090115\"\n        },\n        {\n            \"name\": \"Titan Trust Bank\",\n            \"shortcode\": \"102\",\n            \"longcode\": \"000025\"\n        },\n        {\n            \"name\": \"Union Bank of Nigeria\",\n            \"shortcode\": \"032\",\n            \"longcode\": \"000018\"\n        },\n        {\n            \"name\": \"United Bank For Africa\",\n            \"shortcode\": \"033\",\n            \"longcode\": \"000004\"\n        },\n        {\n            \"name\": \"Unity Bank\",\n            \"shortcode\": \"215\",\n            \"longcode\": \"000011\"\n        },\n        {\n            \"name\": \"VFD\",\n            \"shortcode\": \"566\",\n            \"longcode\": \"090110\"\n        },\n        {\n            \"name\": \"Wema Bank\",\n            \"shortcode\": \"035\",\n            \"longcode\": \"000017\"\n        },\n        {\n            \"name\": \"Zenith Bank\",\n            \"shortcode\": \"057\",\n            \"longcode\": \"000015\"\n        }\n    ],\n    \"meta\": {\n        \"cost\": 0,\n        \"balance\": 1225\n    }\n}"
								}
							]
						},
						{
							"name": "Get Status Check",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}status",
									"host": [
										"{{base_url}}status"
									]
								},
								"description": "This endpoint is used to obtain the status of systems under Adjutor."
							},
							"response": [
								{
									"name": "Get Status Check",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}status",
											"host": [
												"{{base_url}}status"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Mon, 14 Aug 2023 13:18:09 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Transfer-Encoding",
											"value": "chunked"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "2c08234b-24ec-4518-9893-6334a9701fe8"
										},
										{
											"key": "ETag",
											"value": "W/\"323-kZyzG8ZmWrOKUR10s/0qZ95jhMM\""
										},
										{
											"key": "CF-Cache-Status",
											"value": "DYNAMIC"
										},
										{
											"key": "Server",
											"value": "cloudflare"
										},
										{
											"key": "CF-RAY",
											"value": "7f697b679c7fd42c-LOS"
										},
										{
											"key": "Content-Encoding",
											"value": "gzip"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": true,\n    \"data\": [\n        {\n            \"service\": \"adjutor-oraculi-scoring\",\n            \"success\": true\n        },\n        {\n            \"service\": \"adjutor-name-inquiry\",\n            \"success\": false\n        },\n        {\n            \"service\": \"adjutor-name-inquiry-bvn\",\n            \"success\": false\n        },\n        {\n            \"service\": \"adjutor-karma-lookup\",\n            \"success\": true\n        },\n        {\n            \"service\": \"adjutor-bvn-verification\",\n            \"success\": false\n        },\n        {\n            \"service\": \"adjutor-image-compare\",\n            \"success\": true\n        },\n        {\n            \"service\": \"adjutor-ecosystem-lookup\",\n            \"success\": true\n        },\n        {\n            \"service\": \"adjutor-bank-list\",\n            \"success\": true\n        },\n        {\n            \"service\": \"adjutor-crc\",\n            \"success\": false\n        },\n        {\n            \"service\": \"adjutor-firstcentral\",\n            \"success\": false\n        },\n        {\n            \"service\": \"adjutor-credit-registry\",\n            \"success\": false\n        },\n        {\n            \"service\": \"adjutor-oraculi-accounts\",\n            \"success\": true\n        },\n        {\n            \"service\": \"adjutor-oraculi-statement\",\n            \"success\": true\n        },\n        {\n            \"service\": \"adjutor-oraculi-analytics\",\n            \"success\": true\n        },\n        {\n            \"service\": \"adjutor-oraculi-models\",\n            \"success\": true\n        }\n    ]\n}"
								}
							]
						}
					],
					"description": "The Miscellaneous folder contains resources and tools for miscellaneous tasks, such as obtaining bank codes and checking the status of the Adjútor API service to ensure that it is functioning properly. This folder provides a convenient way to access information and troubleshoot any issues, helping you stay informed and in control of your system at all times."
				}
			],
			"description": "These endpoints are a collection of APIs to be used by a lender or an integrator to get information about their accounts, profiles, and wallet balances."
		},
		{
			"name": "Direct Debit",
			"item": [
				{
					"name": "Banks",
					"item": [
						{
							"name": "Get All Banks",
							"event": [
								{
									"listen": "test",
									"script": {
										"exec": [
											"pm.environment.get(\"variable_key\");\r",
											"pm.test(\"Status code is 200\", function () {\r",
											"    pm.response.to.have.status(201);\r",
											"});"
										],
										"type": "text/javascript",
										"packages": {}
									}
								}
							],
							"protocolProfileBehavior": {
								"disableBodyPruning": true
							},
							"request": {
								"method": "GET",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}direct-debit/banks?limit=100&page=1&sort_dir=ASC",
									"host": [
										"{{base_url}}direct-debit"
									],
									"path": [
										"banks"
									],
									"query": [
										{
											"key": "limit",
											"value": "100"
										},
										{
											"key": "page",
											"value": "1"
										},
										{
											"key": "sort_dir",
											"value": "ASC"
										}
									]
								},
								"description": "This endpoints returns the lis of banks able to provide direct debit authorizations on their customers' accounts.\n\n#### Response Body Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| id | `Integer` | Unique identifier for the bank. |\n| name | `string` | Name of the bank. |\n| bank_code | `string` | This is the CBN code associated with the bank. It is usually 3 digits for commercial banks and 5 digits for microfinance banks. |\n| institution_code | `string` | This is the NIBSS code associated with the bank. It is is usually 6 digits long. For commercial banks, the code is in the format 0000XX where X is from 0 to 99. |\n| url | `string` | URL pointing to the bank's logo or image. |"
							},
							"response": [
								{
									"name": "Get All Banks",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"body": {
											"mode": "raw",
											"raw": "",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{base_url}}direct-debit/banks?limit=100&page=1&sort_dir=ASC",
											"host": [
												"{{base_url}}direct-debit"
											],
											"path": [
												"banks"
											],
											"query": [
												{
													"key": "limit",
													"value": "100"
												},
												{
													"key": "page",
													"value": "1"
												},
												{
													"key": "sort_dir",
													"value": "ASC"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "713b4442-1cf6-46bb-8a39-85de0ad54d89"
										},
										{
											"key": "Last-Modified",
											"value": "Wed, 27 Mar 2024 16:28:29 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Content-Length",
											"value": "6395"
										},
										{
											"key": "ETag",
											"value": "W/\"18fb-Pj1/ZMbxWk/ZZFF1vrvEYAOh3tM\""
										},
										{
											"key": "Date",
											"value": "Wed, 27 Mar 2024 16:28:31 GMT"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Keep-Alive",
											"value": "timeout=5"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"success\",\n    \"data\": {\n        \"data\": [\n            {\n                \"id\": 1,\n                \"name\": \"Access Bank\",\n                \"bank_code\": \"044\",\n                \"institution_code\": \"000014\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/044.png\",\n                \"activation_amount\": \"50.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":50,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            },\n            {\n                \"id\": 7,\n                \"name\": \"Ecobank Nigeria\",\n                \"bank_code\": \"050\",\n                \"institution_code\": \"000010\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/050.png\",\n                \"activation_amount\": \"50.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":50,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            },\n            {\n                \"id\": 11,\n                \"name\": \"Fidelity Bank\",\n                \"bank_code\": \"070\",\n                \"institution_code\": \"000007\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/070.png\",\n                \"activation_amount\": \"50.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":50,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            },\n            {\n                \"id\": 10,\n                \"name\": \"First Bank of Nigeria\",\n                \"bank_code\": \"011\",\n                \"institution_code\": \"000016\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/011.png\",\n                \"activation_amount\": \"50.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":50,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            },\n            {\n                \"id\": 12,\n                \"name\": \"First City Monument Bank\",\n                \"bank_code\": \"214\",\n                \"institution_code\": \"000003\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/214.png\",\n                \"activation_amount\": \"50.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":50,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            },\n            {\n                \"id\": 16,\n                \"name\": \"Guaranty Trust Bank\",\n                \"bank_code\": \"058\",\n                \"institution_code\": \"000013\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/058.png\",\n                \"activation_amount\": \"50.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":50,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            },\n            {\n                \"id\": 18,\n                \"name\": \"Keystone Bank\",\n                \"bank_code\": \"082\",\n                \"institution_code\": \"000002\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/082.png\",\n                \"activation_amount\": \"50.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":50,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            },\n            {\n                \"id\": 22,\n                \"name\": \"Kuda Bank\",\n                \"bank_code\": \"50211\",\n                \"institution_code\": \"090267\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/50211.png\",\n                \"activation_amount\": \"50.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":50,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            },\n            {\n                \"id\": 25,\n                \"name\": \"Polaris Bank\",\n                \"bank_code\": \"076\",\n                \"institution_code\": \"000008\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/076.png\",\n                \"activation_amount\": \"50.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":50,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            },\n            {\n                \"id\": 24,\n                \"name\": \"Providus Bank\",\n                \"bank_code\": \"101\",\n                \"institution_code\": \"000023\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/101.png\",\n                \"activation_amount\": \"50.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":50,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            },\n            {\n                \"id\": 27,\n                \"name\": \"Stanbic IBTC Bank\",\n                \"bank_code\": \"221\",\n                \"institution_code\": \"000012\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/221.png\",\n                \"activation_amount\": \"50.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":50,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            },\n            {\n                \"id\": 28,\n                \"name\": \"Standard Chartered Bank\",\n                \"bank_code\": \"068\",\n                \"institution_code\": \"000021\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/068.png\",\n                \"activation_amount\": \"100.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":100,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            },\n            {\n                \"id\": 29,\n                \"name\": \"Sterling Bank\",\n                \"bank_code\": \"232\",\n                \"institution_code\": \"000001\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/232.png\",\n                \"activation_amount\": \"50.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":50,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            },\n            {\n                \"id\": 34,\n                \"name\": \"Suntrust Bank\",\n                \"bank_code\": \"100\",\n                \"institution_code\": \"000022\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/100.png\",\n                \"activation_amount\": \"50.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":50,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            },\n            {\n                \"id\": 36,\n                \"name\": \"Union Bank of Nigeria\",\n                \"bank_code\": \"032\",\n                \"institution_code\": \"000018\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/032.png\",\n                \"activation_amount\": \"100.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":100,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            },\n            {\n                \"id\": 40,\n                \"name\": \"United Bank For Africa\",\n                \"bank_code\": \"033\",\n                \"institution_code\": \"000004\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/033.png\",\n                \"activation_amount\": \"50.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":50,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            },\n            {\n                \"id\": 37,\n                \"name\": \"Unity Bank\",\n                \"bank_code\": \"215\",\n                \"institution_code\": \"000011\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/215.png\",\n                \"activation_amount\": \"100.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":100,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            },\n            {\n                \"id\": 2,\n                \"name\": \"Wema Bank\",\n                \"bank_code\": \"035\",\n                \"institution_code\": \"000017\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/035.png\",\n                \"activation_amount\": \"50.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":50,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            },\n            {\n                \"id\": 41,\n                \"name\": \"Zenith Bank\",\n                \"bank_code\": \"057\",\n                \"institution_code\": \"000015\",\n                \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/057.png\",\n                \"activation_amount\": \"50.00\",\n                \"meta\": \"{\\\"mandate-activation-amount\\\":50,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n            }\n        ],\n        \"meta\": {\n            \"records\": 19,\n            \"page\": \"1\",\n            \"pages\": 1,\n            \"page_size\": \"100\"\n        }\n    },\n    \"meta\": {\n        \"cost\": 1,\n        \"balance\": 1010\n    }\n}"
								}
							]
						},
						{
							"name": "Get Details of a Bank",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}direct-debit/banks/:bank_id",
									"host": [
										"{{base_url}}direct-debit"
									],
									"path": [
										"banks",
										":bank_id"
									],
									"variable": [
										{
											"key": "bank_id",
											"value": "1"
										}
									]
								},
								"description": "Retrieve the details of a specific account.\n\n#### Query Params\n\n| Field | Type | Description |\n| --- | --- | --- |\n| bank_id | `Integer` | **Required**. The ID of the bank you want to get the details of. |\n\n#### Response Body Field\n\n| Field | Type | Description |\n| --- | --- | --- |\n| status | `string` | The status of the response. |\n| message | `string` | A message indicating the result of the operation. |\n| data | `object` | The data object contains specific information related to the response. |\n| ID | `number` | The ID associated with the bank. |\n| bank | `string` | The name of the bank. |\n| bank_code | `string` | The bank code associated with the bank. |\n| institutional_code | `string` | The institution code associated with the bank. |\n| url | `string` | The URL pointing to the bank's logo image |"
							},
							"response": [
								{
									"name": "Get Details of a Bank",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}direct-debit/banks/:bank_id",
											"host": [
												"{{base_url}}direct-debit"
											],
											"path": [
												"banks",
												":bank_id"
											],
											"variable": [
												{
													"key": "bank_id",
													"value": "1"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "c711d34d-4378-472a-a43c-5a603a435c21"
										},
										{
											"key": "Last-Modified",
											"value": "Wed, 27 Mar 2024 16:48:19 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Content-Length",
											"value": "403"
										},
										{
											"key": "ETag",
											"value": "W/\"193-NjjN04voJ7aLorbmK2F0o9mtDHg\""
										},
										{
											"key": "Date",
											"value": "Wed, 27 Mar 2024 16:48:22 GMT"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Keep-Alive",
											"value": "timeout=5"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"success\",\n    \"data\": {\n        \"id\": 1,\n        \"name\": \"Access Bank\",\n        \"bank_code\": \"044\",\n        \"institution_code\": \"000014\",\n        \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/044.png\",\n        \"activation_amount\": \"50.00\",\n        \"meta\": \"{\\\"mandate-activation-amount\\\":50,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n    },\n    \"meta\": {\n        \"cost\": 1,\n        \"balance\": 1010\n    }\n}"
								}
							]
						},
						{
							"name": "Verify Bank Account Number",
							"request": {
								"method": "POST",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"account_number\": \"220000000099\",\n    \"bank_code\": \"057\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}direct-debit/banks/account-lookup",
									"host": [
										"{{base_url}}direct-debit"
									],
									"path": [
										"banks",
										"account-lookup"
									]
								},
								"description": "This endpoint is used to verify the validity and details of a Nigerian account number.\n\n#### Request Body Field\n\n| Field | Type | Description |\n| --- | --- | --- |\n| account_number | `string` | **Required**. A valid `NUBAN` account number which must be 10 digits. |\n| bank_id | `integer` | **Required**. Identifier of the bank to which the account belongs. |\n\n#### Response Body Field\n\n| Field | Type | Description |\n| --- | --- | --- |\n| account_name | `string` | Name of the account holder associated with the account number. |\n| bvn | `string` | Masked Bank Verification Number (BVN) associated with the account holder. If the BVN on the account is 22222222222 then it will be shown as 22000000022 |\n| session_id | `string` | Session ID or identifier associated with the account lookup operation. |"
							},
							"response": [
								{
									"name": "Verify Bank Account Number",
									"originalRequest": {
										"method": "POST",
										"header": [],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"account_number\": \"2150302690\",\n    \"bank_code\": \"057\"\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{base_url}}direct-debit/banks/account-lookup",
											"host": [
												"{{base_url}}direct-debit"
											],
											"path": [
												"banks",
												"account-lookup"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "ea9bc497-d658-4848-9906-d4d2c5274bcf"
										},
										{
											"key": "Last-Modified",
											"value": "Wed, 27 Mar 2024 16:50:07 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Content-Length",
											"value": "186"
										},
										{
											"key": "ETag",
											"value": "W/\"ba-/00MCsOg6ox3KzdLPt8n1Zi280k\""
										},
										{
											"key": "Date",
											"value": "Wed, 27 Mar 2024 16:50:11 GMT"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Keep-Alive",
											"value": "timeout=5"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"success\",\n    \"data\": {\n        \"account_name\": \"vee Test\",\n        \"bvn\": \"220000000099\",\n        \"session_id\": \"999999230427160615129743771734\"\n    },\n    \"meta\": {\n        \"cost\": 1,\n        \"balance\": 1010\n    }\n}"
								}
							]
						}
					],
					"description": "These endpoints are used to get the list of Nigerian banks, details of specific banks. They can also be used to bank account verification.\n\n#### Note\n\nNot all banks are included as some banks have either not implemented their direct debit service, or they return DO NOT HONOR on direct debit requests.\n\nIf a bank is missing, please email [support@lendsqr.com](https://mailto:support@lendsqr.com) for assistance or more details."
				},
				{
					"name": "Mandates",
					"item": [
						{
							"name": "Create Mandate",
							"request": {
								"method": "POST",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"account_number\": \"2017991793\",\n    \"phone_number\": \"08072444975\",\n    \"debit_type\": \"partial\",\n    \"frequency\": \"daily\",\n    \"bank_code\": \"50211\",\n    \"email\": \"jesutomy.oni@gmail.com\",\n    \"number_of_payments\": 5,\n    \"payment_start_date\": \"2024-11-01\",\n    \"start_date\": \"2024-11-01\",\n    \"end_date\": \"2024-12-30\",\n    \"narration\": \"Rand\",\n    \"address\": \"Ikate\",\n    \"invite\": true,\n    \"amount\": 1500,\n    \"minimum_amount\": 1000,\n    \"type\": \"emandate\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}direct-debit/mandates",
									"host": [
										"{{base_url}}direct-debit"
									],
									"path": [
										"mandates"
									]
								},
								"description": "This endpoint allows you to create a mandate on a customer's account. The default mandate type is the emandate, which customer can easily activate by themselves.\n\n#### Creating a manual direct debit mandate\n\nHowever, you can also create a manual mandate, which includes scanned written authorization by the bank.\n\nThe use case for this may be creation of mandates on a joint account requiring more than one signatory or a company account where the company instructions specify how instructions must be handled.\n\nWhen creating a manual mandate, there are a few things to note:\n\n- You must have an irrefutable document from a customer, duly signed off, that provides you with the authorization to create a mandate. This document, which should be a PDF or a PNG, would be converted to Base64 when creating the mandate.\n    \n- The manual mandate is immediate sent to the customer banks. However, banks may delay to approve this, therefore, the customer may have to follow up on their banks to get this approved on the system.\n    \n\n#### Request Body Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| account_number | `string` | **Required.** Customer NUBAN account number to create the mandate against |\n| phone_number | `string` | **Required.** The phone number of the customer. The number should be in the form `08012345678`.  <br>  <br>The customer's bank may validate this phone number against what they have on record. Therefore you are advised to use the number that the customer uses to receive SMS messages from their bank. |\n| debit_type | `string` | **Required.** The type of debit which may be `all` or `partial`.  <br>  <br>When set to `all` the system will try to debit the full amount due and when set to `partial` the system will try as much as possible to debit whatever amount can be recover from the customer account.  <br>  <br>The `partial` method is useful for loan repayments. |\n| frequency | `string` | The frequency of debiting the mandates. (`daily`, `weekly`, `monthly`)  <br>`required` if the |\n| bank_id | `Number` | **Required.** The `id` of the bank of the customer bank, is obtained from the Get Bank endpoint. |\n| email | `string` | **Required.** Customer email address. |\n| start_date | `string` | **Required.** The `start date` of the mandate. A mandate cannot be trigger for transactions before the `start date`. |\n| end_date | `string` | **Required.** The `end date` of the mandate. The mandate will expire on the last day. |\n| narration | `string` | **Required.** The narration or description of the mandate. |\n| address | `string` | **Required.** Customer address. |\n| amount | `Number` | **Required**. The maximum amount that can be debited on the mandate at a single time. However, the total amount debited against a mandate depends on how frequent the API to debit a mandate is called.  <br>  <br>Therefore, in theory, the total amount debited against a mandate may be multiples of the maximum amount that can be debited at once. |\n| schedule | `Boolean` | Indicates whether the transaction is scheduled (true) or not (false). |\n| type | `string` | Indicates whether the mandate is an e-mandate (emandate) or a manual mandate (manual). |\n| file_base64 | `string` | **Required.** The Base64 encoded data equivalent to the customer's mandate letter. |\n| file_extension | `string` | **`optional`****.** The extension of the file that has been added as a base64 data. It is usually `pdf` or `png`. |\n\n#### Response Body Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| id | `Integer` | The ID of the created mandate. |\n| account_number | `string` | The account number associated with the mandate. |\n| reference_number | `string` | A reference number assigned to the mandate. |\n| account_name | `string` | The account name associated with the mandate. |\n| frequency | `string` | The frequency of the mandate (e.g., \"daily\", \"weekly\", \"monthly\"). |\n| bvn | `string` | The Bank Verification Number (BVN) associated with the mandate. |\n| phone_number | `string` | The phone number associated with the mandate. |\n| email | `string` | The email address associated with the mandate. |\n| start_date | `string` | The start date of the mandate. |\n| end_date | `string` | The end date of the mandate. |\n| narration | `string` | The narration or description of the mandate. |\n| address | `string` | The address associated with the mandate. |\n| amount | `string` | The amount associated with the mandate. |\n| status | `string` | The status of the mandate (e.g., \"initiated\", \"active\", \"inactive\"). |\n| workflow_status | `string` | The workflow status of the mandate. |\n| debit_type | `string` | The debit type of the mandate (e.g., \"all\" or \"partial\"). |\n| type | `string` | The type of the mandate (e.g., \"emandate\" or \"manual\"). |\n| schedule | `Boolean` | Indicates whether the transaction is scheduled (true) or not (false). |\n| created_on | `string` | The date and time when the mandate was created in ISO 8601 format. |"
							},
							"response": [
								{
									"name": "Create E-Mandate",
									"originalRequest": {
										"method": "POST",
										"header": [],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"account_number\": \"0123456789\",\n    \"phone_number\": \"08123456789\",\n    \"debit_type\": \"all\",\n    \"frequency\": \"daily\",\n    \"bank_code\": \"057\",\n    \"email\": \"email@example.com\",\n    \"number_of_payments\": 6,\n    \"payment_start_date\": \"2023-11-01\",\n    \"start_date\": \"2023-11-01\",\n    \"end_date\": \"2023-12-30\",\n    \"narration\": \"Rand\",\n    \"address\": \"Ikate\",\n    \"invite\": true,\n    \"amount\": 500,\n    \"type\": \"emandate\"\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{base_url}}direct-debit/mandates",
											"host": [
												"{{base_url}}direct-debit"
											],
											"path": [
												"mandates"
											]
										}
									},
									"status": "Created",
									"code": 201,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Access-Control-Allow-Origin",
											"value": "*"
										},
										{
											"key": "Access-Control-Allow-Credentials",
											"value": "true"
										},
										{
											"key": "Access-Control-Expose-Headers",
											"value": "x-encryption-key,x-encryption-iv"
										},
										{
											"key": "Content-Security-Policy",
											"value": "default-src 'self';base-uri 'self';font-src 'self' https: data:;form-action 'self';frame-ancestors 'self';img-src 'self' data:;object-src 'none';script-src 'self';script-src-attr 'none';style-src 'self' https: 'unsafe-inline';upgrade-insecure-requests"
										},
										{
											"key": "Cross-Origin-Embedder-Policy",
											"value": "require-corp"
										},
										{
											"key": "Cross-Origin-Opener-Policy",
											"value": "same-origin"
										},
										{
											"key": "Cross-Origin-Resource-Policy",
											"value": "same-origin"
										},
										{
											"key": "X-DNS-Prefetch-Control",
											"value": "off"
										},
										{
											"key": "X-Frame-Options",
											"value": "SAMEORIGIN"
										},
										{
											"key": "Strict-Transport-Security",
											"value": "max-age=15552000; includeSubDomains"
										},
										{
											"key": "X-Download-Options",
											"value": "noopen"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "Origin-Agent-Cluster",
											"value": "?1"
										},
										{
											"key": "X-Permitted-Cross-Domain-Policies",
											"value": "none"
										},
										{
											"key": "Referrer-Policy",
											"value": "no-referrer"
										},
										{
											"key": "X-XSS-Protection",
											"value": "0"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Content-Length",
											"value": "701"
										},
										{
											"key": "ETag",
											"value": "W/\"2bd-ZnQe3lfyVlBwwznxkAAsV8MX24A\""
										},
										{
											"key": "Date",
											"value": "Fri, 27 Oct 2023 09:51:54 GMT"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Keep-Alive",
											"value": "timeout=5"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"Mandate created successfully\",\n    \"data\": {\n        \"id\": 55,\n        \"session_id\": \"999999230712125043396550293089\",\n        \"reference_number\": \"RC1153578/1234/999999999\",\n        \"account_number\": \"0123456789\",\n        \"account_name\": \"ADO JOHN SULE\",\n        \"frequency\": \"daily\",\n        \"bvn\": \"\",\n        \"phone_number\": \"08123456789\",\n        \"email\": \"email@example.com\",\n        \"start_date\": \"2023-10-31T23:00:00.000Z\",\n        \"end_date\": \"2023-12-29T23:00:00.000Z\",\n        \"narration\": \"Rand\",\n        \"address\": \"Ikate\",\n        \"minimum_amount\": \"0.00\",\n        \"amount\": \"500.00\",\n        \"status\": \"initiated\",\n        \"schedule\": 0,\n        \"type\": \"emandate\",\n        \"NIBSS_workflow_status\": null,\n        \"NIBSS_workflow_status_description\": null,\n        \"debit_type\": \"all\",\n        \"invite\": true,\n        \"created_on\": \"2023-10-27T08:51:38.000Z\",\n        \"activation_instruction\": \"This emandate is currently in initiated status. To activate, kindly send a N50.00 from the account on which the mandate is set up to undefined at undefined Bank. The activation must be done within 24 hours of set up.\",\n        \"schedules\": []\n    },\n    \"meta\": {\n        \"balance\": 1010\n    }\n}"
								}
							]
						},
						{
							"name": "Get All Mandates",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}direct-debit/mandates?limit=10&page=1",
									"host": [
										"{{base_url}}direct-debit"
									],
									"path": [
										"mandates"
									],
									"query": [
										{
											"key": "limit",
											"value": "10"
										},
										{
											"key": "page",
											"value": "1"
										}
									]
								},
								"description": "This endpoint is used to retrieve mandates or information for a specific mandate. The `reference_number` is the unique mandate ID generated when the mandate was created.\n\n#### Query Params\n\n| Field | Type | Description |\n| --- | --- | --- |\n| reference_number | `number` | **Required.** The reference number of the mandate you want to get the details of. |\n\n#### Response Body Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| file | `number` | **Required.** The reference number of the mandate you want to get the details of. |"
							},
							"response": [
								{
									"name": "Get All Mandates",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}direct-debit/mandates?limit=10&page=1",
											"host": [
												"{{base_url}}direct-debit"
											],
											"path": [
												"mandates"
											],
											"query": [
												{
													"key": "limit",
													"value": "10"
												},
												{
													"key": "page",
													"value": "1"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "c5aac60f-faca-4ef8-b833-c8e33e49d55d"
										},
										{
											"key": "Last-Modified",
											"value": "Thu, 28 Mar 2024 01:39:18 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Content-Length",
											"value": "19847"
										},
										{
											"key": "ETag",
											"value": "W/\"4d87-euutde1hC8uaGi+/KLj9cb0KDrk\""
										},
										{
											"key": "Date",
											"value": "Thu, 28 Mar 2024 01:39:22 GMT"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Keep-Alive",
											"value": "timeout=5"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"success\",\n    \"data\": {\n        \"data\": [\n            {\n                \"id\": 10,\n                \"session_id\": \"999999231016152258600000000000\",\n                \"reference_number\": \"RC00000/1507/000000000000\",\n                \"account_number\": \"2150000090\",\n                \"account_name\": \"TEST ACCOUNT\",\n                \"frequency\": \"daily\",\n                \"bvn\": \"22000000076\",\n                \"phone_number\": \"08130050033\",\n                \"email\": \"email@example.com\",\n                \"start_date\": \"2023-10-31T23:00:00.000Z\",\n                \"end_date\": \"2023-12-29T23:00:00.000Z\",\n                \"narration\": \"Rand\",\n                \"address\": \"Ikate\",\n                \"minimum_amount\": \"0.00\",\n                \"amount\": \"500.00\",\n                \"status\": \"initiated\",\n                \"schedule\": 0,\n                \"type\": \"manual\",\n                \"NIBSS_workflow_status\": null,\n                \"NIBSS_workflow_status_description\": null,\n                \"debit_type\": \"all\",\n                \"created_on\": \"2023-10-16 14:22:59\",\n                \"schedules\": [],\n                \"bank\": {\n                    \"id\": 42,\n                    \"name\": \"Zenith Bank\",\n                    \"bank_code\": \"057\",\n                    \"institution_code\": \"000015\",\n                    \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/057.png\",\n                    \"meta\": {\n                        \"mandate-activation-amount\": 50,\n                        \"mandate-activation-bank\": \"Paystack-Titan\",\n                        \"mandate-activation-account-number\": \"9880218357\"\n                    }\n                },\n                \"beneficiary\": {\n                    \"id\": 2,\n                    \"account_number\": \"54000000000\",\n                    \"account_name\": \"DD OPERATIONS\",\n                    \"bvn\": \".\",\n                    \"last_transaction_date\": null,\n                    \"status\": \"active\",\n                    \"created_on\": \"2023-09-22 15:29:32\",\n                    \"bank\": {\n                        \"id\": 24,\n                        \"name\": \"Providus Bank\",\n                        \"bank_code\": \"101\",\n                        \"institution_code\": \"000023\",\n                        \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/101.png\"\n                    }\n                },\n                \"activation_instruction\": \"This mandate is currently in initiated status. To activate, the bank direct debit officers need to log into the NIBSS CMMS platform to authorize or approve. The customer may also call their bank account manager for more details.\"\n            }\n        ],\n        \"meta\": {\n            \"records\": 1,\n            \"page\": \"1\",\n            \"pages\": 1,\n            \"page_size\": \"10\"\n        }\n    },\n    \"meta\": {\n        \"cost\": 1,\n        \"balance\": 1010\n    }\n}"
								}
							]
						},
						{
							"name": "Get Mandate Details",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}direct-debit/mandates?reference_number={{reference_number}}",
									"host": [
										"{{base_url}}direct-debit"
									],
									"path": [
										"mandates"
									],
									"query": [
										{
											"key": "reference_number",
											"value": "{{reference_number}}"
										}
									]
								},
								"description": "Retrieves the details of a specific mandate.\n\n#### Query Params\n\n| Field | Type | Description |\n| --- | --- | --- |\n| reference_number | `string` | **Required.** The reference number of the mandate you want to get the details of. |\n\n#### Response Body Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| account_number | `string` | The account number associated with the mandate. |\n| account_name | `string` | The account name associated with the mandate. |\n| frequency | `string` | The frequency of the mandate (e.g., \"daily\", \"weekly\", \"monthly\"). |\n| bvn | `string` | The Bank Verification Number (BVN) associated with the mandate. |\n| phone_number | `string` | The phone number associated with the mandate. |\n| email | `string` | The email address associated with the mandate. |\n| start_date | `string` | The start date of the mandate. |\n| end_date | `string` | The end date of the mandate. |\n| narration | `string` | The narration or description of the mandate. |\n| address | `string` | The address associated with the mandate. |\n| amount | `string` | The amount associated with the mandate. |\n| status | `string` | The status of the mandate (e.g., \"initiated\", \"active\", \"inactive\", \"pending\"). |\n| workflow_status | `string` | The workflow status of the mandate. |\n| debit_type | `string` | The debit type of the mandate (e.g., \"All\" and \"Partial\"). |\n| created_on | `string` | The date and time when the mandate was created. |\n| bank.name | `string` | The name of the bank associated with the mandate. |\n| bank.bank_code | `string` | The bank code of the bank associated with the mandate. |\n| bank.institution_code | `string` | The institution code of the bank associated with the mandate. |\n| bank.url | `string` | The URL of the bank associated with the mandate. |"
							},
							"response": [
								{
									"name": "Get Mandate Details",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}direct-debit/mandates?reference_number={{reference_number}}",
											"host": [
												"{{base_url}}direct-debit"
											],
											"path": [
												"mandates"
											],
											"query": [
												{
													"key": "reference_number",
													"value": "{{reference_number}}"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "e6e32b70-8398-481c-92d0-88f44d86443c"
										},
										{
											"key": "Last-Modified",
											"value": "Thu, 28 Mar 2024 01:43:32 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Content-Length",
											"value": "1955"
										},
										{
											"key": "ETag",
											"value": "W/\"7a3-tUM5qNNXuFjp/db/6nT7xLHaYkA\""
										},
										{
											"key": "Date",
											"value": "Thu, 28 Mar 2024 01:43:36 GMT"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Keep-Alive",
											"value": "timeout=5"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"success\",\n    \"data\": {\n        \"data\": [\n            {\n                \"id\": 29,\n                \"session_id\": \"999999230614194314842810401824\",\n                \"reference_number\": \"0000004/001/999999999\",\n                \"account_number\": \"0123456789\",\n                \"account_name\": \"vee Test\",\n                \"frequency\": \"daily\",\n                \"bvn\": \"220000000099\",\n                \"phone_number\": \"0123456789\",\n                \"email\": \"email@example.com\",\n                \"start_date\": \"2023-01-01\",\n                \"end_date\": \"2025-12-31\",\n                \"narration\": \"Rand\",\n                \"address\": \"Ikate\",\n                \"minimum_amount\": \"0.00\",\n                \"amount\": \"50.00\",\n                \"status\": \"inactive\",\n                \"workflow_status\": \"2\",\n                \"debit_type\": \"all\",\n                \"created_on\": \"2023-06-14 19:43:20\",\n                \"bank\": {\n                    \"id\": 42,\n                    \"name\": \"Zenith Bank\",\n                    \"bank_code\": \"057\",\n                    \"institution_code\": \"000015\",\n                    \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/057.png\",\n                    \"meta\": {\n                        \"mandate-activation-amount\": 50,\n                        \"mandate-activation-bank\": \"Paystack-Titan\",\n                        \"mandate-activation-account-number\": \"9880218357\"\n                    }\n                },\n                \"activation_instruction\": \"This mandate is currently in initiated status. To activate, the bank direct debit officers need to log into the NIBSS CMMS platform to authorize or approve. The customer may also call their bank account manager for more details.\"\n            }\n        ],\n        \"meta\": {\n            \"records\": 1,\n            \"page\": 1,\n            \"pages\": 1,\n            \"page_size\": 10\n        }\n    },\n    \"meta\": {\n        \"cost\": 1,\n        \"balance\": 1010\n    }\n}"
								}
							]
						},
						{
							"name": "Get Mandate Summary",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}direct-debit/mandates/stats",
									"host": [
										"{{base_url}}direct-debit"
									],
									"path": [
										"mandates",
										"stats"
									]
								},
								"description": "This endpoints provides the summary of all mandates within the system.\n\n#### Response Body Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| status | `string` | Mandate status (e.g., active, inactive) |\n| count | `number` | The count of each mandate status. |\n| data | `array` | An array containing objects with status and count information for different mandate statuses. |"
							},
							"response": []
						},
						{
							"name": "Cancel a mandate",
							"request": {
								"method": "PATCH",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"reference_number\": \"0000004/001/0000073969\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}direct-debit/mandates/cancel",
									"host": [
										"{{base_url}}direct-debit"
									],
									"path": [
										"mandates",
										"cancel"
									]
								},
								"description": "Updates the status of a mandate\n\n#### Query Params\n\n| Field | Type | Description |\n| --- | --- | --- |\n| type | `string` | **Required**.The status you want to update the mandate. (`activate`/`deactivate)` to which |\n\n#### Body Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| reference_number | `string` | The reference number of the mandate to activate or deactivate |\n\n#### Response Body Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| status | `string` | The status of the response. |\n| message | `string` | A message indicating the result of the update. |"
							},
							"response": [
								{
									"name": "Cancel a Mandate",
									"originalRequest": {
										"method": "PATCH",
										"header": [],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"reference_number\": \"0000004/001/0000073969\"\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{base_url}}direct-debit/mandates/cancel",
											"host": [
												"{{base_url}}direct-debit"
											],
											"path": [
												"mandates",
												"cancel"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Access-Control-Allow-Origin",
											"value": "*"
										},
										{
											"key": "Access-Control-Allow-Credentials",
											"value": "true"
										},
										{
											"key": "Access-Control-Expose-Headers",
											"value": "x-encryption-key,x-encryption-iv"
										},
										{
											"key": "Content-Security-Policy",
											"value": "default-src 'self';base-uri 'self';font-src 'self' https: data:;form-action 'self';frame-ancestors 'self';img-src 'self' data:;object-src 'none';script-src 'self';script-src-attr 'none';style-src 'self' https: 'unsafe-inline';upgrade-insecure-requests"
										},
										{
											"key": "Cross-Origin-Embedder-Policy",
											"value": "require-corp"
										},
										{
											"key": "Cross-Origin-Opener-Policy",
											"value": "same-origin"
										},
										{
											"key": "Cross-Origin-Resource-Policy",
											"value": "same-origin"
										},
										{
											"key": "X-DNS-Prefetch-Control",
											"value": "off"
										},
										{
											"key": "X-Frame-Options",
											"value": "SAMEORIGIN"
										},
										{
											"key": "Strict-Transport-Security",
											"value": "max-age=15552000; includeSubDomains"
										},
										{
											"key": "X-Download-Options",
											"value": "noopen"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "Origin-Agent-Cluster",
											"value": "?1"
										},
										{
											"key": "X-Permitted-Cross-Domain-Policies",
											"value": "none"
										},
										{
											"key": "Referrer-Policy",
											"value": "no-referrer"
										},
										{
											"key": "X-XSS-Protection",
											"value": "0"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Content-Length",
											"value": "40"
										},
										{
											"key": "ETag",
											"value": "W/\"28-OVMgSyV1oMqtVb/r7kZWp0D/aOk\""
										},
										{
											"key": "Date",
											"value": "Mon, 23 Oct 2023 06:55:25 GMT"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Keep-Alive",
											"value": "timeout=5"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"success\",\n    \"meta\": {\n        \"balance\": 1010\n    }\n}"
								}
							]
						},
						{
							"name": "Debit a Mandate",
							"request": {
								"method": "POST",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"reference_number\": \"0000004/001/0000073969\",\n    \"amount\": 40,\n    \"narration\": \"This is a test narration\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}direct-debit/mandates/debit",
									"host": [
										"{{base_url}}direct-debit"
									],
									"path": [
										"mandates",
										"debit"
									]
								},
								"description": "This endpoint enables you to perform a debit on a customer's account using an authorized mandate. For this to happen, these are the prerequisites:\n\n- The mandate must have been created on the profile of that the API credentials are attached to\n- The mandate must have been authorized or validated by the customer's bank\n- The mandate start date must be in the past and the expiry date in the future\n    \n\nFor a mandate to be debited successfully:\n\n- The customer's account must be in good standing at their bank. For example, their bank account cannot be dormant\n- The customer's account must have enough funds to carry the debit. Mandates cannot force debit an account\n    \n\n#### Request Body Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| reference_number | String | **Required.** The reference number assigned to the mandate. |\n| amount | Number | **Required.** The amount to be debited on the mandate. |\n\n#### Response Body Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| status | String | The overall status of the response. |\n| message | String | A message providing additional information about the response status. For example, \"Mandate debited successfully\". |\n| status | String | The status of the specific mandate transaction. Possible values: \"successful\", \"failed\", etc. |\n| amount | String | The amount debited in the mandate transaction. |\n| reference | String | A unique reference identifier for the mandate transaction. |"
							},
							"response": [
								{
									"name": "Debit Mandate",
									"originalRequest": {
										"method": "POST",
										"header": [],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"reference_number\": \"0000004/001/0000073969\",\n    \"amount\": 500\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{base_url}}direct-debit/mandates/debit",
											"host": [
												"{{base_url}}direct-debit"
											],
											"path": [
												"mandates",
												"debit"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Wed, 19 Jul 2023 16:58:00 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Content-Length",
											"value": "143"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Server",
											"value": "openresty"
										},
										{
											"key": "X-RateLimit-Limit",
											"value": "1000"
										},
										{
											"key": "X-RateLimit-Remaining",
											"value": "996"
										},
										{
											"key": "Access-Control-Allow-Origin",
											"value": "*"
										},
										{
											"key": "Access-Control-Allow-Credentials",
											"value": "true"
										},
										{
											"key": "Access-Control-Expose-Headers",
											"value": "x-encryption-key,x-encryption-iv"
										},
										{
											"key": "Content-Security-Policy",
											"value": "default-src 'self';base-uri 'self';font-src 'self' https: data:;form-action 'self';frame-ancestors 'self';img-src 'self' data:;object-src 'none';script-src 'self';script-src-attr 'none';style-src 'self' https: 'unsafe-inline';upgrade-insecure-requests"
										},
										{
											"key": "Cross-Origin-Embedder-Policy",
											"value": "require-corp"
										},
										{
											"key": "Cross-Origin-Opener-Policy",
											"value": "same-origin"
										},
										{
											"key": "Cross-Origin-Resource-Policy",
											"value": "same-origin"
										},
										{
											"key": "X-DNS-Prefetch-Control",
											"value": "off"
										},
										{
											"key": "X-Frame-Options",
											"value": "SAMEORIGIN"
										},
										{
											"key": "Strict-Transport-Security",
											"value": "max-age=15552000; includeSubDomains"
										},
										{
											"key": "X-Download-Options",
											"value": "noopen"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "Origin-Agent-Cluster",
											"value": "?1"
										},
										{
											"key": "X-Permitted-Cross-Domain-Policies",
											"value": "none"
										},
										{
											"key": "Referrer-Policy",
											"value": "no-referrer"
										},
										{
											"key": "X-XSS-Protection",
											"value": "0"
										},
										{
											"key": "ETag",
											"value": "W/\"8f-Ua6YyVhqZrS5Mi38nnlKRyEIgsE\""
										},
										{
											"key": "Age",
											"value": "9"
										},
										{
											"key": "Via",
											"value": "http/1.1 api-umbrella (ApacheTrafficServer [cMsSf ])"
										},
										{
											"key": "X-Cache",
											"value": "MISS"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"Mandate debited successfully\",\n    \"data\": {\n        \"status\": \"successful\",\n        \"amount\": \"500.00\",\n        \"reference\": \"DD-SHFhaf1ycS80gG5\"\n    },\n    \"meta\": {\n        \"balance\": 1010\n    }\n}"
								}
							]
						},
						{
							"name": "Check Account Balance",
							"request": {
								"method": "POST",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"reference_number\": \"0000004/001/0000073969\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}direct-debit/banks/balance-lookup",
									"host": [
										"{{base_url}}direct-debit"
									],
									"path": [
										"banks",
										"balance-lookup"
									]
								},
								"description": "Retrieves the balance of the account associated with a mandate\n\nNote: This has been suspended temporarily by NIBSS.\n\n#### Request Body Field\n\n| Field | Type | Description |\n| --- | --- | --- |\n| reference_number | String | **Required**. A reference number assigned to the mandate. |\n\n#### Response Body Field\n\n| Field | Type | Description |\n| --- | --- | --- |\n| status | String | The overall status of the response |\n| message | String | A message providing additional information about the response status. |\n| balance | Number | The account balance value. |"
							},
							"response": [
								{
									"name": "Balance Lookup",
									"originalRequest": {
										"method": "POST",
										"header": [],
										"body": {
											"mode": "raw",
											"raw": "{\n    \"reference_number\": \"0000004/001/0000073969\"\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{base_url}}direct-debit/banks/balance-lookup",
											"host": [
												"{{base_url}}direct-debit"
											],
											"path": [
												"banks",
												"balance-lookup"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "Date",
											"value": "Thu, 20 Jul 2023 17:07:15 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Content-Length",
											"value": "52"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Server",
											"value": "openresty"
										},
										{
											"key": "X-RateLimit-Limit",
											"value": "1000"
										},
										{
											"key": "X-RateLimit-Remaining",
											"value": "991"
										},
										{
											"key": "Access-Control-Allow-Origin",
											"value": "*"
										},
										{
											"key": "Access-Control-Allow-Credentials",
											"value": "true"
										},
										{
											"key": "Access-Control-Expose-Headers",
											"value": "x-encryption-key,x-encryption-iv"
										},
										{
											"key": "Content-Security-Policy",
											"value": "default-src 'self';base-uri 'self';font-src 'self' https: data:;form-action 'self';frame-ancestors 'self';img-src 'self' data:;object-src 'none';script-src 'self';script-src-attr 'none';style-src 'self' https: 'unsafe-inline';upgrade-insecure-requests"
										},
										{
											"key": "Cross-Origin-Embedder-Policy",
											"value": "require-corp"
										},
										{
											"key": "Cross-Origin-Opener-Policy",
											"value": "same-origin"
										},
										{
											"key": "Cross-Origin-Resource-Policy",
											"value": "same-origin"
										},
										{
											"key": "X-DNS-Prefetch-Control",
											"value": "off"
										},
										{
											"key": "X-Frame-Options",
											"value": "SAMEORIGIN"
										},
										{
											"key": "Strict-Transport-Security",
											"value": "max-age=15552000; includeSubDomains"
										},
										{
											"key": "X-Download-Options",
											"value": "noopen"
										},
										{
											"key": "X-Content-Type-Options",
											"value": "nosniff"
										},
										{
											"key": "Origin-Agent-Cluster",
											"value": "?1"
										},
										{
											"key": "X-Permitted-Cross-Domain-Policies",
											"value": "none"
										},
										{
											"key": "Referrer-Policy",
											"value": "no-referrer"
										},
										{
											"key": "X-XSS-Protection",
											"value": "0"
										},
										{
											"key": "ETag",
											"value": "W/\"34-/OD9Mkr2oMb6kI5JzrqiWEkDqrM\""
										},
										{
											"key": "Age",
											"value": "2"
										},
										{
											"key": "Via",
											"value": "http/1.1 api-umbrella (ApacheTrafficServer [cMs f ])"
										},
										{
											"key": "X-Cache",
											"value": "MISS"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"success\",\n    \"data\": {\n        \"balance\": 22785.71\n    },\n    \"meta\": {\n        \"balance\": 1010\n    }\n}"
								}
							]
						}
					]
				},
				{
					"name": "Transactions",
					"item": [
						{
							"name": "Get All Transactions",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}direct-debit/transactions?limit=10&page=1",
									"host": [
										"{{base_url}}direct-debit"
									],
									"path": [
										"transactions"
									],
									"query": [
										{
											"key": "limit",
											"value": "10"
										},
										{
											"key": "page",
											"value": "1"
										}
									]
								},
								"description": "Retrieve the transactions related to the mandates associated with the API key.\n\n#### Response Body Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| id | `integer` | The ID of the transaction. |\n| amount | String | The amount of the transaction. |\n| mandate_id | `integer` | The ID of the associated mandate. |\n| mandate_account_name | String | The account name associated with the mandate. |\n| mandate_account_number | `integer` | The account number associated with the mandate. |\n| mandate_bvn | String | The Bank Verification Number (BVN) associated with the mandate. |\n| reference | String | The reference number of the transaction. |\n| narration | String | The description or purpose of the transaction. |\n| beneficiary_id | `integer` | The ID of the recipient of the mandate debits. |\n| beneficiary_account_name | String | The account name of the recipient of the mandate debits. |\n| beneficiary_account_number | `integer` | The account number of the recipient of the mandate debits. |\n| beneficiary_bvn | String | The Bank Verification Number (BVN) of the beneficiary. |\n| session_id | String | The session ID associated with the transaction. |\n| status | String | The status of the transaction (e.g., success, failed). |\n| created_on | String | The date and time when the transaction was created. |\n| mandate_bank | `object` | The bank details associated with the mandate (see bank fields below). |\n\n#### Mandate Bank Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| id | `integer` | The ID of the bank. |\n| name | String | The name of the bank. |\n| bank_code | String | The bank code associated with the bank. |\n| institution_code | String | The institution code associated with the bank. |\n| url | String | The URL of the bank (if available). |"
							},
							"response": [
								{
									"name": "Get All Transactions",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}direct-debit/transactions?limit=10&page=1",
											"host": [
												"{{base_url}}direct-debit"
											],
											"path": [
												"transactions"
											],
											"query": [
												{
													"key": "limit",
													"value": "10"
												},
												{
													"key": "page",
													"value": "1"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "9c990955-2d05-463a-9968-8d8ef8aef90d"
										},
										{
											"key": "Last-Modified",
											"value": "Wed, 27 Mar 2024 17:05:10 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Content-Length",
											"value": "7731"
										},
										{
											"key": "ETag",
											"value": "W/\"1e33-JscIFlPIDztpaYzPXGIWueotanI\""
										},
										{
											"key": "Date",
											"value": "Wed, 27 Mar 2024 17:05:13 GMT"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Keep-Alive",
											"value": "timeout=5"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"success\",\n    \"data\": {\n        \"data\": [\n            {\n                \"id\": 15,\n                \"amount\": \"500\",\n                \"mandate_id\": 7,\n                \"mandate_account_name\": \"vee Test\",\n                \"mandate_account_number\": \"1780004070\",\n                \"mandate_bvn\": \"22222222222\",\n                \"reference\": \"DD-cU26qsOsdGCSGn\",\n                \"narration\": \"Direct Debit Transfer\",\n                \"session_id\": \"999999230920215225299534241477\",\n                \"status\": \"successful\",\n                \"created_on\": \"2023-05-11 07:07:01\",\n                \"mandate_bank\": {\n                    \"name\": \"Test Bank 1\",\n                    \"bank_code\": \"998\",\n                    \"institution_code\": \"999998\",\n                    \"url\": null\n                },\n                \"mandate\": {\n                    \"reference_number\": \"RC1145578/1599/000000000\"\n                }\n            },\n            {\n                \"id\": 14,\n                \"amount\": \"500\",\n                \"mandate_id\": 7,\n                \"mandate_account_name\": \"vee Test\",\n                \"mandate_account_number\": \"1780004070\",\n                \"mandate_bvn\": \"22222222222\",\n                \"reference\": \"DD-cU26qsO05mGCSGn\",\n                \"narration\": \"Direct Debit Transfer\",\n                \"session_id\": \"999999230920215225299534241477\",\n                \"status\": \"successful\",\n                \"created_on\": \"2023-05-11 07:07:01\",\n                \"mandate_bank\": {\n                    \"name\": \"Test Bank 1\",\n                    \"bank_code\": \"998\",\n                    \"institution_code\": \"999998\",\n                    \"url\": null\n                },\n                \"mandate\": {\n                    \"reference_number\": \"RC1145578/1599/000000000\"\n                }\n            },\n            {\n                \"id\": 13,\n                \"amount\": \"500\",\n                \"mandate_id\": 7,\n                \"mandate_account_name\": \"vee Test\",\n                \"mandate_account_number\": \"1780004070\",\n                \"mandate_bvn\": \"22222222222\",\n                \"reference\": \"DD-cU26qsdmGCSgGn\",\n                \"narration\": \"Direct Debit Transfer\",\n                \"session_id\": \"999999230920215225299534241477\",\n                \"status\": \"successful\",\n                \"created_on\": \"2023-05-11 07:07:01\",\n                \"mandate_bank\": {\n                    \"name\": \"Test Bank 1\",\n                    \"bank_code\": \"998\",\n                    \"institution_code\": \"999998\",\n                    \"url\": null\n                },\n                \"mandate\": {\n                    \"reference_number\": \"RC1145578/1599/000000000\"\n                }\n            },\n            {\n                \"id\": 12,\n                \"amount\": \"500\",\n                \"mandate_id\": 7,\n                \"mandate_account_name\": \"vee Test\",\n                \"mandate_account_number\": \"1780004070\",\n                \"mandate_bvn\": \"22222222222\",\n                \"reference\": \"DD-cU26qsO05mGCSGn\",\n                \"narration\": \"Direct Debit Transfer\",\n                \"session_id\": \"999999230920215225299534241477\",\n                \"status\": \"successful\",\n                \"created_on\": \"2023-05-11 07:07:01\",\n                \"mandate_bank\": {\n                    \"name\": \"Test Bank 1\",\n                    \"bank_code\": \"998\",\n                    \"institution_code\": \"999998\",\n                    \"url\": null\n                },\n                \"mandate\": {\n                    \"reference_number\": \"RC1145578/1599/000000000\"\n                }\n            },\n            {\n                \"id\": 11,\n                \"amount\": \"500\",\n                \"mandate_id\": 7,\n                \"mandate_account_name\": \"vee Test\",\n                \"mandate_account_number\": \"1780004070\",\n                \"mandate_bvn\": \"22222222222\",\n                \"reference\": \"DD-cU26qsO05mGCSGn\",\n                \"narration\": \"Direct Debit Transfer\",\n                \"session_id\": \"999999230920215225299534241477\",\n                \"status\": \"successful\",\n                \"created_on\": \"2023-05-11 07:07:01\",\n                \"mandate_bank\": {\n                    \"name\": \"Test Bank 1\",\n                    \"bank_code\": \"998\",\n                    \"institution_code\": \"999998\",\n                    \"url\": null\n                },\n                \"mandate\": {\n                    \"reference_number\": \"RC1145578/1599/000000000\"\n                }\n            },\n            {\n                \"id\": 10,\n                \"amount\": \"500\",\n                \"mandate_id\": 7,\n                \"mandate_account_name\": \"vee Test\",\n                \"mandate_account_number\": \"1780004070\",\n                \"mandate_bvn\": \"22222222222\",\n                \"reference\": \"DD-cU26qsO05mGCSGn\",\n                \"narration\": \"Direct Debit Transfer\",\n                \"session_id\": \"999999230920215225299534241477\",\n                \"status\": \"successful\",\n                \"created_on\": \"2023-05-11 07:07:01\",\n                \"mandate_bank\": {\n                    \"name\": \"Test Bank 1\",\n                    \"bank_code\": \"998\",\n                    \"institution_code\": \"999998\",\n                    \"url\": null\n                },\n                \"mandate\": {\n                    \"reference_number\": \"RC1145578/1599/000000000\"\n                }\n            },\n            {\n                \"id\": 9,\n                \"amount\": \"500\",\n                \"mandate_id\": 7,\n                \"mandate_account_name\": \"vee Test\",\n                \"mandate_account_number\": \"1780004070\",\n                \"mandate_bvn\": \"22222222222\",\n                \"reference\": \"DD-cU26qsO05mGCSGn\",\n                \"narration\": \"Direct Debit Transfer\",\n                \"session_id\": \"999999230920215225299534241477\",\n                \"status\": \"successful\",\n                \"created_on\": \"2023-05-11 07:07:01\",\n                \"mandate_bank\": {\n                    \"name\": \"Test Bank 1\",\n                    \"bank_code\": \"998\",\n                    \"institution_code\": \"999998\",\n                    \"url\": null\n                },\n                \"mandate\": {\n                    \"reference_number\": \"RC1145578/1599/000000000\"\n                }\n            },\n            {\n                \"id\": 8,\n                \"amount\": \"500\",\n                \"mandate_id\": 7,\n                \"mandate_account_name\": \"vee Test\",\n                \"mandate_account_number\": \"1780004070\",\n                \"mandate_bvn\": \"22222222222\",\n                \"reference\": \"DD-cU26qsO05mGCSGn\",\n                \"narration\": \"Direct Debit Transfer\",\n                \"session_id\": \"999999230920215225299534241477\",\n                \"status\": \"successful\",\n                \"created_on\": \"2023-05-11 07:07:01\",\n                \"mandate_bank\": {\n                    \"name\": \"Test Bank 1\",\n                    \"bank_code\": \"998\",\n                    \"institution_code\": \"999998\",\n                    \"url\": null\n                },\n                \"mandate\": {\n                    \"reference_number\": \"RC1145578/1599/000000000\"\n                }\n            },\n            {\n                \"id\": 7,\n                \"amount\": \"500\",\n                \"mandate_id\": 7,\n                \"mandate_account_name\": \"vee Test\",\n                \"mandate_account_number\": \"1780004070\",\n                \"mandate_bvn\": \"22222222222\",\n                \"reference\": \"DD-cU26qsO05mGCSGn\",\n                \"narration\": \"Direct Debit Transfer\",\n                \"session_id\": \"999999230920215225299534241477\",\n                \"status\": \"successful\",\n                \"created_on\": \"2023-05-11 07:07:01\",\n                \"mandate_bank\": {\n                    \"name\": \"Test Bank 1\",\n                    \"bank_code\": \"998\",\n                    \"institution_code\": \"999998\",\n                    \"url\": null\n                },\n                \"mandate\": {\n                    \"reference_number\": \"RC1145578/1599/000000000\"\n                }\n            },\n            {\n                \"id\": 6,\n                \"amount\": \"500\",\n                \"mandate_id\": 7,\n                \"mandate_account_name\": \"vee Test\",\n                \"mandate_account_number\": \"1780004070\",\n                \"mandate_bvn\": \"22222222222\",\n                \"reference\": \"DD-cU26qsO05mGCSGn\",\n                \"narration\": \"Direct Debit Transfer\",\n                \"session_id\": \"999999230920215225299534241477\",\n                \"status\": \"successful\",\n                \"created_on\": \"2023-05-11 07:07:01\",\n                \"mandate_bank\": {\n                    \"name\": \"Test Bank 1\",\n                    \"bank_code\": \"998\",\n                    \"institution_code\": \"999998\",\n                    \"url\": null\n                },\n                \"mandate\": {\n                    \"reference_number\": \"RC1145578/1599/000000000\"\n                }\n            }\n        ],\n        \"meta\": {\n            \"records\": 15,\n            \"page\": \"1\",\n            \"pages\": 2,\n            \"page_size\": \"10\"\n        }\n    },\n    \"meta\": {\n        \"cost\": 1,\n        \"balance\": 1010\n    }\n}"
								}
							]
						},
						{
							"name": "Get Details of a Transaction",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}direct-debit/transactions?reference=DD-cU26qsO05mGCSGn",
									"host": [
										"{{base_url}}direct-debit"
									],
									"path": [
										"transactions"
									],
									"query": [
										{
											"key": "reference",
											"value": "DD-cU26qsO05mGCSGn"
										}
									]
								},
								"description": "Retrieves the details of a specific transaction.\n\n#### Params Query\n\n| Field | Type | Description |\n| --- | --- | --- |\n| reference | String | **Required**. The reference number of the mandate transaction you want to get the details of. |\n\n#### Response Body Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| id | `integer` | The ID of the transaction. |\n| amount | String | The amount of the transaction. |\n| mandate_id | `integer` | The ID of the associated mandate. |\n| mandate_account_name | String | The account name associated with the mandate. |\n| mandate_account_number | `integer` | The account number associated with the mandate. |\n| mandate_bvn | String | The Bank Verification Number (BVN) associated with the mandate. |\n| reference | String | The reference number of the transaction. |\n| narration | String | The description or purpose of the transaction. |\n| beneficiary_id | `integer` | The ID of the recipient of the mandate debits. |\n| beneficiary_account_name | String | The account name of the recipient of the mandate debits. |\n| beneficiary_account_number | `integer` | The account number of the recipient of the mandate debits. |\n| beneficiary_bvn | String | The Bank Verification Number (BVN) of the beneficiary. |\n| session_id | String | The session ID associated with the transaction. |\n| status | String | The status of the transaction (e.g., success, failed). |\n| created_on | String | The date and time when the transaction was created. |\n| mandate_bank | `object` | The bank details associated with the mandate (see bank fields below). |\n\n##### Mandate Bank Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| id | `integer` | The ID of the bank. |\n| name | String | The name of the bank. |\n| bank_code | String | The bank code associated with the bank. |\n| institution_code | String | The institution code associated with the bank. |\n| url | String | The URL of the bank (if available). |"
							},
							"response": [
								{
									"name": "Get Details of a Transaction",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}direct-debit/transactions?reference=DD-WCo3KTTUn1dZgAV",
											"host": [
												"{{base_url}}direct-debit"
											],
											"path": [
												"transactions"
											],
											"query": [
												{
													"key": "reference",
													"value": "DD-WCo3KTTUn1dZgAV"
												}
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "203650f6-fee5-4452-baec-6779de722573"
										},
										{
											"key": "Last-Modified",
											"value": "Wed, 27 Mar 2024 17:07:36 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Content-Length",
											"value": "904"
										},
										{
											"key": "ETag",
											"value": "W/\"388-xErTWr+FkJV09fWlwB7b45G78l4\""
										},
										{
											"key": "Date",
											"value": "Wed, 27 Mar 2024 17:07:38 GMT"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Keep-Alive",
											"value": "timeout=5"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"success\",\n    \"data\": {\n        \"data\": [\n            {\n                \"id\": 2592,\n                \"amount\": \"250.00\",\n                \"mandate_id\": 478,\n                \"mandate_account_name\": \"AKINSANYA ADEOLUWA OLORUNTOMI\",\n                \"mandate_account_number\": \"0421008622\",\n                \"mandate_bvn\": \"22000000076\",\n                \"reference\": \"DD-WCo3KTTUn1dZgAV\",\n                \"narration\": \"Direct debit for mandate schedule 699\",\n                \"session_id\": \"110069240327000044440000237994\",\n                \"status\": \"failed\",\n                \"created_on\": \"2024-03-26 23:00:35\",\n                \"mandate_bank\": {\n                    \"id\": 16,\n                    \"name\": \"Guaranty Trust Bank\",\n                    \"bank_code\": \"058\",\n                    \"institution_code\": \"000013\",\n                    \"url\": \"https://lendstack-s3.s3.us-east-2.amazonaws.com/bank_logos/058.png\",\n                    \"activation_amount\": \"50.00\",\n                    \"meta\": \"{\\\"mandate-activation-amount\\\":50,\\\"mandate-activation-bank\\\":\\\"Paystack-Titan\\\",\\\"mandate-activation-account-number\\\":\\\"9880218357\\\"}\"\n                },\n                \"mandate\": {\n                    \"reference_number\": \"RC1544159/1517/0001380571\"\n                }\n            }\n        ],\n        \"meta\": {\n            \"records\": 1,\n            \"page\": 1,\n            \"pages\": 1,\n            \"page_size\": 10\n        }\n    },\n    \"meta\": {\n        \"cost\": 1,\n        \"balance\": 1010\n    }\n}"
								}
							]
						},
						{
							"name": "Get Transactions Statistics",
							"request": {
								"method": "GET",
								"header": [
									{
										"key": "Authorization",
										"value": "Bearer {{TOKEN}}",
										"type": "text"
									}
								],
								"url": {
									"raw": "{{base_url}}direct-debit/transactions/stats",
									"host": [
										"{{base_url}}direct-debit"
									],
									"path": [
										"transactions",
										"stats"
									]
								},
								"description": "Retrieves the status of transactions associated with the API key.\n\n#### Response Body Fields\n\n| Field | Type | Description |\n| --- | --- | --- |\n| status | String | The status of the mandate transactions. |\n| count | `integer` | The number of transactions with the given status. |"
							},
							"response": [
								{
									"name": "Get Transactions Statistics",
									"originalRequest": {
										"method": "GET",
										"header": [
											{
												"key": "Authorization",
												"value": "Bearer {{TOKEN}}",
												"type": "text"
											}
										],
										"url": {
											"raw": "{{base_url}}direct-debit/transactions/stats",
											"host": [
												"{{base_url}}direct-debit"
											],
											"path": [
												"transactions",
												"stats"
											]
										}
									},
									"status": "OK",
									"code": 200,
									"_postman_previewlanguage": "json",
									"header": [
										{
											"key": "X-Powered-By",
											"value": "Express"
										},
										{
											"key": "X-Request-ID",
											"value": "c83440b7-01c1-42a4-820e-b6245d9ce099"
										},
										{
											"key": "Last-Modified",
											"value": "Wed, 27 Mar 2024 19:06:19 GMT"
										},
										{
											"key": "Content-Type",
											"value": "application/json; charset=utf-8"
										},
										{
											"key": "Content-Length",
											"value": "241"
										},
										{
											"key": "ETag",
											"value": "W/\"f1-1aQUzxdJeUage6Rli20oLe1CC2I\""
										},
										{
											"key": "Date",
											"value": "Wed, 27 Mar 2024 19:06:22 GMT"
										},
										{
											"key": "Connection",
											"value": "keep-alive"
										},
										{
											"key": "Keep-Alive",
											"value": "timeout=5"
										}
									],
									"cookie": [],
									"body": "{\n    \"status\": \"success\",\n    \"message\": \"success\",\n    \"data\": {\n        \"transactions\": [\n            {\n                \"status\": \"total\",\n                \"count\": 36,\n                \"sum\": \"8850.00\"\n            },\n            {\n                \"status\": \"successful\",\n                \"count\": 1,\n                \"sum\": \"100.00\"\n            },\n            {\n                \"status\": \"failed\",\n                \"count\": 35,\n                \"sum\": \"8750.00\"\n            }\n        ]\n    },\n    \"meta\": {\n        \"cost\": 1,\n        \"balance\": 1010\n    }\n}"
								}
							]
						}
					]
				},
				{
					"name": "Webhooks",
					"item": [
						{
							"name": "Mandate Webhook",
							"request": {
								"method": "POST",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\n  \"id\": 2,\n  \"type\": \"mandate\",\n  \"timestamp\": \"2023-10-16T12:36:24.000Z\",\n  \"data\": {\n    \"amount\": \"500.00\",\n    \"status\": \"initiated\",\n    \"reference\": \"1544159/1000/000000000000\",\n    \"narration\": \"Rand\",\n    \"start_date\": \"2023-10-31T23:00:00.000Z\",\n    \"end_date\": \"2023-12-29T23:00:00.000Z\",\n    \"account_number\": \"1010101010\",\n    \"account_name\": \"TEST ACCOUNT\"\n  }\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{webhookUrl}}",
									"host": [
										"{{webhookUrl}}"
									]
								}
							},
							"response": []
						},
						{
							"name": "Transaction Webhook",
							"request": {
								"method": "POST",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\n  \"id\": 5,\n  \"type\": \"transaction\",\n  \"timestamp\": \"2023-10-16T12:36:24.000Z\",\n  \"data\": {\n    \"amount\": \"500.00\",\n    \"status\": \"successful\",\n    \"reference\": \"DD-wdsu82udjws\",\n    \"narration\": \"Rand\",\n    \"transaction_date\": \"2023-10-31T23:00:00.000Z\"\n  }\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{webhookUrl}}",
									"host": [
										"{{webhookUrl}}"
									]
								}
							},
							"response": []
						}
					]
				}
			],
			"description": "## Getting started\n\nDirect debit is a payment method that allows an account holder to grant authorization for a biller or lender to take money from their bank account for services as of when due. Direct debit is similar to debit cards in its ability to debit a customer’s account with prior authorization.\n\nDirect debit helps businesses that require recurring payments on specific dates with fixed amounts, such as insurance premiums, loan repayments, service subscriptions, or variable recurring payments on different dates (e.g., postpaid lines, and electricity usage).\n\nThis direct debit API facilitates the process for Service Providers (referred to as Billers) to generate debit mandate instructions on their client's/customers' bank accounts for services rendered or products sold.\n\nThese debit mandate instructions are created as digital versions of physical instructions duly signed by the account owners (clients/customers). Once generated, the mandate instructions are automatically sent to the bank where the account is held for review and approval. The approval process requires the bank to contact the account owner to authorize the mandate, which typically takes 24 to 48 hours.\n\nThe system automatically assigns a unique mandate code to each initiated mandate. This mandate code is used to initiate a direct debit transaction on the bank account associated with the debit mandate instruction.\n\nThis document provides a comprehensive overview and detailed specifications of the Direct Debit APIs, including all the necessary information for seamless integration into your respective applications.\n\n## Direct debit process\n\nDirect debit mandates follow a streamlined process that may take at least 2 hours from activation to when they are available for debits. These steps are:\n\n- Mandate creation\n- Mandate activation\n- Setup for debit\n- Transactions\n    \n\n### Mandate creation\n\nThe first step is the creation of mandate using the API defined in this collection. As soon as the mandate is created, you should inform the customer of the next steps about how to activate the mandate.\n\nFrom a best practices point of view, the customer should be informed on your app, by email, and SMS.\n\n### Mandate activation\n\nActivation of the mandate is usually done by the transfer of a N50 (or N100 for banks where the minimum transfer amount is N100) to designated bank accounts operated by NIBSS. The customer has 168 hours (7 days) to send this amount if not the mandate is automatically canceled.\n\nImmediately the activation amount is received at either of the banks, the mandate is automatically activated. However, it is not available for debit at this time.\n\n#### Banks for mandate activation\n\nThe following are the authorized banks which customers should use for direct debit mandate activation.\n\n| **Fidelity Bank** | **Paystack Titan** |\n| --- | --- |\n| Account: 9020025928  <br>Bank: Fidelity Bank Plc.  <br>You can transfer from USSD, mobile app or internet banking | Account: 9880218357  <br>Bank: Paystack-Titan  <br>You can transfer from your mobile app and internet banking |\n\n### Setup for debit\n\nThere are usually some backend processes done by NIBSS that then processes the accounts for debit and this may take up to 2 hours before completion. If you try to debit the mandate before this time, it would return an error message such as \"do not honor\"."
		},
		{
			"name": "Kolo Transaction Data [Beta]",
			"item": [
				{
					"name": "Initialize Auth",
					"request": {
						"method": "GET",
						"header": [],
						"url": {
							"raw": "https://app.kolo.finance/data-share?response_type=code&client_id=your_client_id&redirect_uri=redirect_uri&scope=transaction:list transaction:view",
							"protocol": "https",
							"host": [
								"app",
								"kolo",
								"finance"
							],
							"path": [
								"data-share"
							],
							"query": [
								{
									"key": "response_type",
									"value": "code"
								},
								{
									"key": "client_id",
									"value": "your_client_id"
								},
								{
									"key": "redirect_uri",
									"value": "redirect_uri"
								},
								{
									"key": "scope",
									"value": "transaction:list transaction:view"
								}
							]
						},
						"description": "To access the Kolo API, you need to initialize the authorization process. This involves obtaining an authorization code, which can then be exchanged for an access token."
					},
					"response": [
						{
							"name": "Initialize Auth",
							"originalRequest": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "https://app.kolo.finance/data-share?response_type=code&client_id=e2f2ce02-c9f3-4621-9b05-9a8824f43b95&redirect_uri=https://belhope.lsq.app&scope=transaction:list%20transaction:view",
									"protocol": "https",
									"host": [
										"app",
										"kolo",
										"finance"
									],
									"path": [
										"data-share"
									],
									"query": [
										{
											"key": "response_type",
											"value": "code"
										},
										{
											"key": "client_id",
											"value": "e2f2ce02-c9f3-4621-9b05-9a8824f43b95"
										},
										{
											"key": "redirect_uri",
											"value": "https://belhope.lsq.app"
										},
										{
											"key": "scope",
											"value": "transaction:list%20transaction:view"
										}
									]
								}
							},
							"_postman_previewlanguage": "Text",
							"header": null,
							"cookie": [],
							"body": null
						}
					]
				},
				{
					"name": "Exchange Code",
					"request": {
						"auth": {
							"type": "bearer",
							"bearer": [
								{
									"key": "token",
									"value": "sk_live_YtotSQjsdN0XMUIfV2Ur9znewMeolqI7vLrcYYu3",
									"type": "string"
								}
							]
						},
						"method": "POST",
						"header": [],
						"body": {
							"mode": "raw",
							"raw": "{\n    \"redirect_uri\": \"https://starcash.lsq.app\",\n    \"grant_type\": \"authorization_code\",\n    \"code\": \"JMab8BXnAhnCL6J1\"\n}",
							"options": {
								"raw": {
									"language": "json"
								}
							}
						},
						"url": {
							"raw": "{{base_url}}kolo/auth",
							"host": [
								"{{base_url}}kolo"
							],
							"path": [
								"auth"
							]
						},
						"description": "Use this endpoint to exchange an authorization code for an access token. With the access token gotten from the response body, you can go ahead to call the other Kolo endpoints. This is to ensure that the customer has provided you with the complete consent to view their data."
					},
					"response": [
						{
							"name": "Exchange Code",
							"originalRequest": {
								"method": "POST",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"redirect_uri\": \"https://belhope.lsq.app\",\n    \"grant_type\": \"authorization_code\",\n    \"code\": \"kEhA1fQsT86ZxCqh\"\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}kolo/auth",
									"host": [
										"{{base_url}}kolo"
									],
									"path": [
										"auth"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "X-Powered-By",
									"value": "Express"
								},
								{
									"key": "X-Request-ID",
									"value": "916cb700-6bf0-40e9-9cbb-6ead65be72a8"
								},
								{
									"key": "Last-Modified",
									"value": "Thu, 20 Jun 2024 14:11:30 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json; charset=utf-8"
								},
								{
									"key": "Content-Length",
									"value": "800"
								},
								{
									"key": "ETag",
									"value": "W/\"320-NaqaYYz/P66sX2nMknkFsQMRyT8\""
								},
								{
									"key": "Date",
									"value": "Thu, 20 Jun 2024 14:11:35 GMT"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Keep-Alive",
									"value": "timeout=5"
								}
							],
							"cookie": [],
							"body": "{\n    \"access_token\": \"VeIInXBornQSZKAAhcGwxjhgVA3vyR8xYmBmrikN0iQcwiZbqGVvkYTeHPfH2F4J2sT2GLruiLjsZ3BI9IwIaEOFEVGubblGnuTQl0QNptyoohiR2DpZJmcc5QyhYHJ7kNdlYTJgK2fHddembOsGwBJSyXfvehll9zQQHVtmsrKtUODEwbaIKkZ1gFu9TjJpSfFR9ddcm9j2ozJgjns0mQ5TjHKHdZJpSFKVlG1dX21v36mINY7JIBatp2NlE7\",\n    \"refresh_token\": \"5yOpJCqj2XBsQq4qSb8YRQM2g4iSIqyKeKyK9QwOa06wPyVoPyo4f9FCAMS4tIE5XtdOwPBm4bZrhOyU580CzmMGmagCkzM7Mz04SAnHCtMbDYdhqRj3UllnphbbwkTycRpQlXAoBz86hAJhlSMRHE0vl8SbcUUxm0u0kqg8pxyGtxtOQeBoY2ghQnU313oc1SQ9tovb3De2QJNE5TWUWuE6sT0Cuw2kd4cDa98dG9xyR3wL3HVVbSpK9MCfuM\",\n    \"username\": \"adewunmiakinsanya@gmail.com\",\n    \"scope\": \"bank_account:list bank_account:add bank_account:view bank_account:delete bank_account:update bank_account:sync transaction:list transaction:view transaction:update profile:view\",\n    \"token_type\": \"Bearer\"\n}"
						}
					]
				},
				{
					"name": "List Transactions",
					"request": {
						"method": "GET",
						"header": [
							{
								"key": "x-access-token",
								"value": "{{x_access_token}}",
								"type": "text"
							}
						],
						"url": {
							"raw": "{{base_url}}kolo/transactions",
							"host": [
								"{{base_url}}kolo"
							],
							"path": [
								"transactions"
							]
						},
						"description": "Use this endpoint to get a list of all the transactions of an authenticated customer."
					},
					"response": [
						{
							"name": "List Transactions",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "x-access-token",
										"value": "{{x_access_token}}",
										"type": "text"
									}
								],
								"url": {
									"raw": "{{base_url}}kolo/transactions",
									"host": [
										"{{base_url}}kolo"
									],
									"path": [
										"transactions"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "X-Powered-By",
									"value": "Express"
								},
								{
									"key": "X-Request-ID",
									"value": "a2408669-0f07-430c-858d-86969a561f9a"
								},
								{
									"key": "Last-Modified",
									"value": "Thu, 20 Jun 2024 14:14:47 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json; charset=utf-8"
								},
								{
									"key": "Content-Length",
									"value": "11706"
								},
								{
									"key": "ETag",
									"value": "W/\"2dba-LOY5ItnqKmLaIHZst1KW822pj00\""
								},
								{
									"key": "Date",
									"value": "Thu, 20 Jun 2024 14:14:52 GMT"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Keep-Alive",
									"value": "timeout=5"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"success\",\n    \"data\": [\n        {\n            \"id\": \"c954f391-83a6-4265-bf7a-e9e1d2db5013\",\n            \"account_number\": \"2208667061\",\n            \"currency\": \"NGN\",\n            \"amount\": \"10.00\",\n            \"balance\": \"436.56\",\n            \"reference\": \"\",\n            \"hash\": \"{\\\"account_number\\\":\\\"2208667061\\\",\\\"bank_code\\\":\\\"057\\\",\\\"amount\\\":10,\\\"balance\\\":436,\\\"type\\\":\\\"credit\\\",\\\"date\\\":\\\"2024-06-08T15:03:00Z\\\"}\",\n            \"status\": \"success\",\n            \"entry_type\": \"credit\",\n            \"narration\": \"NIP/ROLEZ/Transfer/Transfer to Adewunmi O Akinsanya/***7/AT5_MFDS110202406081601\",\n            \"transaction_date\": \"2024-06-08T15:02:10.000Z\",\n            \"transaction_type\": \"Credit\",\n            \"note\": null,\n            \"source\": \"email\",\n            \"provider\": \"google\",\n            \"bank\": {\n                \"id\": \"d645920e395fedad7bbbed0eca3fe2e0\",\n                \"name\": \"Zenith Bank\",\n                \"short_code\": \"057\",\n                \"long_code\": \"057\",\n                \"icon\": \"https://s3.us-east-2.amazonaws.com/kolo.finance/assets/zenithbank-logo-circle.png\"\n            },\n            \"created_on\": \"2024-06-14T19:00:07.070Z\",\n            \"created_by\": null,\n            \"modified_on\": \"2024-06-14T19:00:07.000Z\",\n            \"modified_by\": null,\n            \"deleted_on\": null,\n            \"deleted_by\": null\n        },\n        {\n            \"id\": \"a1b92539-058b-4768-82fe-24d1a538ded6\",\n            \"account_number\": \"2208667061\",\n            \"currency\": \"NGN\",\n            \"amount\": \"100.00\",\n            \"balance\": \"426.56\",\n            \"reference\": \"\",\n            \"hash\": \"{\\\"account_number\\\":\\\"2208667061\\\",\\\"bank_code\\\":\\\"057\\\",\\\"amount\\\":100,\\\"balance\\\":426,\\\"type\\\":\\\"credit\\\",\\\"date\\\":\\\"2024-06-08T14:54:00Z\\\"}\",\n            \"status\": \"success\",\n            \"entry_type\": \"credit\",\n            \"narration\": \"NIP/ROLEZ/Transfer/Transfer to Adewunmi O Akinsanya/***7/AT5_MFDS655202406081555\",\n            \"transaction_date\": \"2024-06-08T14:55:29.000Z\",\n            \"transaction_type\": \"Credit\",\n            \"note\": null,\n            \"source\": \"email\",\n            \"provider\": \"google\",\n            \"bank\": {\n                \"id\": \"d645920e395fedad7bbbed0eca3fe2e0\",\n                \"name\": \"Zenith Bank\",\n                \"short_code\": \"057\",\n                \"long_code\": \"057\",\n                \"icon\": \"https://s3.us-east-2.amazonaws.com/kolo.finance/assets/zenithbank-logo-circle.png\"\n            },\n            \"created_on\": \"2024-06-08T14:59:37.607Z\",\n            \"created_by\": null,\n            \"modified_on\": \"2024-06-08T14:59:37.000Z\",\n            \"modified_by\": null,\n            \"deleted_on\": null,\n            \"deleted_by\": null\n        },\n        {\n            \"id\": \"456449b1-97be-4235-9003-4d45e023924b\",\n            \"account_number\": \"2208667061\",\n            \"currency\": \"NGN\",\n            \"amount\": \"100.00\",\n            \"balance\": \"333.89\",\n            \"reference\": \"\",\n            \"hash\": \"{\\\"account_number\\\":\\\"2208667061\\\",\\\"bank_code\\\":\\\"057\\\",\\\"amount\\\":100,\\\"balance\\\":333,\\\"type\\\":\\\"credit\\\",\\\"date\\\":\\\"2024-03-27T08:24:00Z\\\"}\",\n            \"status\": \"success\",\n            \"entry_type\": \"credit\",\n            \"narration\": \"NIP/ROLEZ/Transfer/Transfer to Adewunmi O Akinsanya/***70/AT5_MFDS92202403270924\",\n            \"transaction_date\": \"2024-03-27T08:25:01.000Z\",\n            \"transaction_type\": \"Credit\",\n            \"note\": null,\n            \"source\": \"email\",\n            \"provider\": \"google\",\n            \"bank\": {\n                \"id\": \"d645920e395fedad7bbbed0eca3fe2e0\",\n                \"name\": \"Zenith Bank\",\n                \"short_code\": \"057\",\n                \"long_code\": \"057\",\n                \"icon\": \"https://s3.us-east-2.amazonaws.com/kolo.finance/assets/zenithbank-logo-circle.png\"\n            },\n            \"created_on\": \"2024-04-12T15:08:28.485Z\",\n            \"created_by\": null,\n            \"modified_on\": \"2024-04-12T15:08:28.000Z\",\n            \"modified_by\": null,\n            \"deleted_on\": null,\n            \"deleted_by\": null\n        },\n        {\n            \"id\": \"1d86ac44-d61d-423a-8037-9ca0ce6b65ad\",\n            \"account_number\": \"2208667061\",\n            \"currency\": \"NGN\",\n            \"amount\": \"100.00\",\n            \"balance\": \"233.89\",\n            \"reference\": \"\",\n            \"hash\": \"{\\\"account_number\\\":\\\"2208667061\\\",\\\"bank_code\\\":\\\"057\\\",\\\"amount\\\":100,\\\"balance\\\":233,\\\"type\\\":\\\"credit\\\",\\\"date\\\":\\\"2024-03-10T21:03:00Z\\\"}\",\n            \"status\": \"success\",\n            \"entry_type\": \"credit\",\n            \"narration\": \"NIP/STBC/KREDI MONEY MICROFINANCE BANK LIMITED/090380/Transfer to Adewunmi O Aki\",\n            \"transaction_date\": \"2024-03-10T21:03:53.000Z\",\n            \"transaction_type\": \"Credit\",\n            \"note\": null,\n            \"source\": \"email\",\n            \"provider\": \"google\",\n            \"bank\": {\n                \"id\": \"d645920e395fedad7bbbed0eca3fe2e0\",\n                \"name\": \"Zenith Bank\",\n                \"short_code\": \"057\",\n                \"long_code\": \"057\",\n                \"icon\": \"https://s3.us-east-2.amazonaws.com/kolo.finance/assets/zenithbank-logo-circle.png\"\n            },\n            \"created_on\": \"2024-04-12T15:08:28.485Z\",\n            \"created_by\": null,\n            \"modified_on\": \"2024-04-12T15:08:28.000Z\",\n            \"modified_by\": null,\n            \"deleted_on\": null,\n            \"deleted_by\": null\n        },\n        {\n            \"id\": \"b5c1dd80-f28c-44be-9418-1cda44acd5c0\",\n            \"account_number\": \"2208667061\",\n            \"currency\": \"NGN\",\n            \"amount\": \"10.00\",\n            \"balance\": \"133.89\",\n            \"reference\": \"\",\n            \"hash\": \"{\\\"account_number\\\":\\\"2208667061\\\",\\\"bank_code\\\":\\\"057\\\",\\\"amount\\\":10,\\\"balance\\\":133,\\\"type\\\":\\\"credit\\\",\\\"date\\\":\\\"2024-03-10T16:21:00Z\\\"}\",\n            \"status\": \"success\",\n            \"entry_type\": \"credit\",\n            \"narration\": \"NIP/ROLEZ/Transfer/Transfer to Adewunmi O Akinsanya/***7/AT5_MFDS741202403101721\",\n            \"transaction_date\": \"2024-03-10T16:22:10.000Z\",\n            \"transaction_type\": \"Credit\",\n            \"note\": null,\n            \"source\": \"email\",\n            \"provider\": \"google\",\n            \"bank\": {\n                \"id\": \"d645920e395fedad7bbbed0eca3fe2e0\",\n                \"name\": \"Zenith Bank\",\n                \"short_code\": \"057\",\n                \"long_code\": \"057\",\n                \"icon\": \"https://s3.us-east-2.amazonaws.com/kolo.finance/assets/zenithbank-logo-circle.png\"\n            },\n            \"created_on\": \"2024-04-12T15:08:28.485Z\",\n            \"created_by\": null,\n            \"modified_on\": \"2024-04-12T15:08:28.000Z\",\n            \"modified_by\": null,\n            \"deleted_on\": null,\n            \"deleted_by\": null\n        },\n        {\n            \"id\": \"48225422-f6fe-4207-ab27-b97f7f756f30\",\n            \"account_number\": \"2208667061\",\n            \"currency\": \"NGN\",\n            \"amount\": \"1000.00\",\n            \"balance\": \"133.57\",\n            \"reference\": \"\",\n            \"hash\": \"{\\\"account_number\\\":\\\"2208667061\\\",\\\"bank_code\\\":\\\"057\\\",\\\"amount\\\":1000,\\\"balance\\\":133,\\\"type\\\":\\\"debit\\\",\\\"date\\\":\\\"2024-02-16T09:39:00Z\\\"}\",\n            \"status\": \"success\",\n            \"entry_type\": \"debit\",\n            \"narration\": \"Airtime//2348089722636//airtel\",\n            \"transaction_date\": \"2024-02-16T09:39:12.000Z\",\n            \"transaction_type\": \"Airtime\",\n            \"note\": null,\n            \"source\": \"email\",\n            \"provider\": \"google\",\n            \"bank\": {\n                \"id\": \"d645920e395fedad7bbbed0eca3fe2e0\",\n                \"name\": \"Zenith Bank\",\n                \"short_code\": \"057\",\n                \"long_code\": \"057\",\n                \"icon\": \"https://s3.us-east-2.amazonaws.com/kolo.finance/assets/zenithbank-logo-circle.png\"\n            },\n            \"created_on\": \"2024-04-12T15:08:28.485Z\",\n            \"created_by\": null,\n            \"modified_on\": \"2024-04-12T15:08:28.000Z\",\n            \"modified_by\": null,\n            \"deleted_on\": null,\n            \"deleted_by\": null\n        },\n        {\n            \"id\": \"2c69b94b-81a3-46e4-8309-1198172a0de9\",\n            \"account_number\": \"2208667061\",\n            \"currency\": \"NGN\",\n            \"amount\": \"100.00\",\n            \"balance\": \"1133.57\",\n            \"reference\": \"\",\n            \"hash\": \"{\\\"account_number\\\":\\\"2208667061\\\",\\\"bank_code\\\":\\\"057\\\",\\\"amount\\\":100,\\\"balance\\\":1133,\\\"type\\\":\\\"credit\\\",\\\"date\\\":\\\"2024-02-15T23:39:00Z\\\"}\",\n            \"status\": \"success\",\n            \"entry_type\": \"credit\",\n            \"narration\": \"NIP/ROLEZ/Transfer/Transfer to Adewunmi O Akinsanya/***7/AT5_MFDS402202402160035\",\n            \"transaction_date\": \"2024-02-15T23:37:58.000Z\",\n            \"transaction_type\": \"Credit\",\n            \"note\": null,\n            \"source\": \"email\",\n            \"provider\": \"google\",\n            \"bank\": {\n                \"id\": \"d645920e395fedad7bbbed0eca3fe2e0\",\n                \"name\": \"Zenith Bank\",\n                \"short_code\": \"057\",\n                \"long_code\": \"057\",\n                \"icon\": \"https://s3.us-east-2.amazonaws.com/kolo.finance/assets/zenithbank-logo-circle.png\"\n            },\n            \"created_on\": \"2024-04-12T15:08:28.485Z\",\n            \"created_by\": null,\n            \"modified_on\": \"2024-04-12T15:08:28.000Z\",\n            \"modified_by\": null,\n            \"deleted_on\": null,\n            \"deleted_by\": null\n        },\n        {\n            \"id\": \"1f06206a-43c2-4dfe-a308-297022a61f74\",\n            \"account_number\": \"2208667061\",\n            \"currency\": \"NGN\",\n            \"amount\": \"100.00\",\n            \"balance\": \"1033.57\",\n            \"reference\": \"\",\n            \"hash\": \"{\\\"account_number\\\":\\\"2208667061\\\",\\\"bank_code\\\":\\\"057\\\",\\\"amount\\\":100,\\\"balance\\\":1033,\\\"type\\\":\\\"credit\\\",\\\"date\\\":\\\"2024-02-06T18:33:00Z\\\"}\",\n            \"status\": \"success\",\n            \"entry_type\": \"credit\",\n            \"narration\": \"NIP/STLB/ADEWUNMI AKINSANYA/Transfer from ADEWUNMI AKINSANYA to ADEWUNMI O AKINS\",\n            \"transaction_date\": \"2024-02-06T18:33:44.000Z\",\n            \"transaction_type\": \"Credit\",\n            \"note\": null,\n            \"source\": \"email\",\n            \"provider\": \"google\",\n            \"bank\": {\n                \"id\": \"d645920e395fedad7bbbed0eca3fe2e0\",\n                \"name\": \"Zenith Bank\",\n                \"short_code\": \"057\",\n                \"long_code\": \"057\",\n                \"icon\": \"https://s3.us-east-2.amazonaws.com/kolo.finance/assets/zenithbank-logo-circle.png\"\n            },\n            \"created_on\": \"2024-04-12T15:08:28.485Z\",\n            \"created_by\": null,\n            \"modified_on\": \"2024-04-12T15:08:28.000Z\",\n            \"modified_by\": null,\n            \"deleted_on\": null,\n            \"deleted_by\": null\n        },\n        {\n            \"id\": \"cb690351-de1c-4053-bc8c-b5298281c808\",\n            \"account_number\": \"2208667061\",\n            \"currency\": \"NGN\",\n            \"amount\": \"50.00\",\n            \"balance\": \"963.51\",\n            \"reference\": \"\",\n            \"hash\": \"{\\\"account_number\\\":\\\"2208667061\\\",\\\"bank_code\\\":\\\"057\\\",\\\"amount\\\":50,\\\"balance\\\":963,\\\"type\\\":\\\"credit\\\",\\\"date\\\":\\\"2024-01-11T08:33:00Z\\\"}\",\n            \"status\": \"success\",\n            \"entry_type\": \"credit\",\n            \"narration\": \"NIP/ROLEZ/Transfer/Transfer to Adewunmi O Akinsanya/***7/AT5_MFDS963202401110932\",\n            \"transaction_date\": \"2024-01-11T08:32:46.000Z\",\n            \"transaction_type\": \"Credit\",\n            \"note\": null,\n            \"source\": \"email\",\n            \"provider\": \"google\",\n            \"bank\": {\n                \"id\": \"d645920e395fedad7bbbed0eca3fe2e0\",\n                \"name\": \"Zenith Bank\",\n                \"short_code\": \"057\",\n                \"long_code\": \"057\",\n                \"icon\": \"https://s3.us-east-2.amazonaws.com/kolo.finance/assets/zenithbank-logo-circle.png\"\n            },\n            \"created_on\": \"2024-04-12T15:08:28.485Z\",\n            \"created_by\": null,\n            \"modified_on\": \"2024-04-12T15:08:28.000Z\",\n            \"modified_by\": null,\n            \"deleted_on\": null,\n            \"deleted_by\": null\n        },\n        {\n            \"id\": \"5d0d4d61-e044-444d-970b-e89e399482ef\",\n            \"account_number\": \"2208667061\",\n            \"currency\": \"NGN\",\n            \"amount\": \"100.00\",\n            \"balance\": \"819.44\",\n            \"reference\": \"\",\n            \"hash\": \"{\\\"account_number\\\":\\\"2208667061\\\",\\\"bank_code\\\":\\\"057\\\",\\\"amount\\\":100,\\\"balance\\\":819,\\\"type\\\":\\\"credit\\\",\\\"date\\\":\\\"2023-11-29T21:27:00Z\\\"}\",\n            \"status\": \"success\",\n            \"entry_type\": \"credit\",\n            \"narration\": \"NIP/KUDA/ADEWUNMI OLADIPUPO AKINSANYA/TEST\",\n            \"transaction_date\": \"2023-11-29T21:27:30.000Z\",\n            \"transaction_type\": \"Credit\",\n            \"note\": null,\n            \"source\": \"email\",\n            \"provider\": \"google\",\n            \"bank\": {\n                \"id\": \"d645920e395fedad7bbbed0eca3fe2e0\",\n                \"name\": \"Zenith Bank\",\n                \"short_code\": \"057\",\n                \"long_code\": \"057\",\n                \"icon\": \"https://s3.us-east-2.amazonaws.com/kolo.finance/assets/zenithbank-logo-circle.png\"\n            },\n            \"created_on\": \"2024-04-12T15:08:28.485Z\",\n            \"created_by\": null,\n            \"modified_on\": \"2024-04-12T15:08:28.000Z\",\n            \"modified_by\": null,\n            \"deleted_on\": null,\n            \"deleted_by\": null\n        },\n        {\n            \"id\": \"4aab533c-e467-44c5-bcbc-fed5e64d7f96\",\n            \"account_number\": \"2208667061\",\n            \"currency\": \"NGN\",\n            \"amount\": \"100.00\",\n            \"balance\": \"719.44\",\n            \"reference\": \"\",\n            \"hash\": \"{\\\"account_number\\\":\\\"2208667061\\\",\\\"bank_code\\\":\\\"057\\\",\\\"amount\\\":100,\\\"balance\\\":719,\\\"type\\\":\\\"credit\\\",\\\"date\\\":\\\"2023-11-29T20:54:00Z\\\"}\",\n            \"status\": \"success\",\n            \"entry_type\": \"credit\",\n            \"narration\": \"NIP/KUDA/ADEWUNMI OLADIPUPO AKINSANYA/TEST\",\n            \"transaction_date\": \"2023-11-29T20:54:50.000Z\",\n            \"transaction_type\": \"Credit\",\n            \"note\": null,\n            \"source\": \"email\",\n            \"provider\": \"google\",\n            \"bank\": {\n                \"id\": \"d645920e395fedad7bbbed0eca3fe2e0\",\n                \"name\": \"Zenith Bank\",\n                \"short_code\": \"057\",\n                \"long_code\": \"057\",\n                \"icon\": \"https://s3.us-east-2.amazonaws.com/kolo.finance/assets/zenithbank-logo-circle.png\"\n            },\n            \"created_on\": \"2024-04-12T15:08:28.485Z\",\n            \"created_by\": null,\n            \"modified_on\": \"2024-04-12T15:08:28.000Z\",\n            \"modified_by\": null,\n            \"deleted_on\": null,\n            \"deleted_by\": null\n        },\n        {\n            \"id\": \"da46acdf-c6ac-4e3d-bb36-8881aa1d9cdc\",\n            \"account_number\": \"2208667061\",\n            \"currency\": \"NGN\",\n            \"amount\": \"100.00\",\n            \"balance\": \"623.44\",\n            \"reference\": \"\",\n            \"hash\": \"{\\\"account_number\\\":\\\"2208667061\\\",\\\"bank_code\\\":\\\"057\\\",\\\"amount\\\":100,\\\"balance\\\":623,\\\"type\\\":\\\"credit\\\",\\\"date\\\":\\\"2023-11-21T10:42:00Z\\\"}\",\n            \"status\": \"success\",\n            \"entry_type\": \"credit\",\n            \"narration\": \"NIP/KUDA/ADEWUNMI OLADIPUPO AKINSANYA/TEST AGAIN\",\n            \"transaction_date\": \"2023-11-21T10:42:50.000Z\",\n            \"transaction_type\": \"Credit\",\n            \"note\": null,\n            \"source\": \"email\",\n            \"provider\": \"google\",\n            \"bank\": {\n                \"id\": \"d645920e395fedad7bbbed0eca3fe2e0\",\n                \"name\": \"Zenith Bank\",\n                \"short_code\": \"057\",\n                \"long_code\": \"057\",\n                \"icon\": \"https://s3.us-east-2.amazonaws.com/kolo.finance/assets/zenithbank-logo-circle.png\"\n            },\n            \"created_on\": \"2024-04-12T15:08:28.485Z\",\n            \"created_by\": null,\n            \"modified_on\": \"2024-04-12T15:08:28.000Z\",\n            \"modified_by\": null,\n            \"deleted_on\": null,\n            \"deleted_by\": null\n        },\n        {\n            \"id\": \"a0d7dbf7-6387-4c5c-8271-8e42d14c5501\",\n            \"account_number\": \"2208667061\",\n            \"currency\": \"NGN\",\n            \"amount\": \"100.00\",\n            \"balance\": \"525.36\",\n            \"reference\": \"\",\n            \"hash\": \"{\\\"account_number\\\":\\\"2208667061\\\",\\\"bank_code\\\":\\\"057\\\",\\\"amount\\\":100,\\\"balance\\\":525,\\\"type\\\":\\\"credit\\\",\\\"date\\\":\\\"2023-10-13T23:45:00Z\\\"}\",\n            \"status\": \"success\",\n            \"entry_type\": \"credit\",\n            \"narration\": \"NIP/STBC/KREDI MONEY MICROFINANCE BANK LIMITED/090380/Transfer to ADEWUNMI O AKI\",\n            \"transaction_date\": \"2023-10-13T23:44:00.000Z\",\n            \"transaction_type\": \"Credit\",\n            \"note\": null,\n            \"source\": \"email\",\n            \"provider\": \"google\",\n            \"bank\": {\n                \"id\": \"d645920e395fedad7bbbed0eca3fe2e0\",\n                \"name\": \"Zenith Bank\",\n                \"short_code\": \"057\",\n                \"long_code\": \"057\",\n                \"icon\": \"https://s3.us-east-2.amazonaws.com/kolo.finance/assets/zenithbank-logo-circle.png\"\n            },\n            \"created_on\": \"2024-04-12T15:08:28.485Z\",\n            \"created_by\": null,\n            \"modified_on\": \"2024-04-12T15:08:28.000Z\",\n            \"modified_by\": null,\n            \"deleted_on\": null,\n            \"deleted_by\": null\n        }\n    ],\n    \"meta\": {\n        \"cost\": 0,\n        \"balance\": 585\n    }\n}"
						}
					]
				},
				{
					"name": "Get Transaction",
					"request": {
						"method": "GET",
						"header": [
							{
								"key": "x-access-token",
								"value": "{{x_access_token}}",
								"type": "text"
							}
						],
						"url": {
							"raw": "{{base_url}}kolo/transactions/:id",
							"host": [
								"{{base_url}}kolo"
							],
							"path": [
								"transactions",
								":id"
							],
							"variable": [
								{
									"key": "id",
									"value": "c954f391-83a6-4265-bf7a-e9e1d2db5013"
								}
							]
						},
						"description": "Use this endpoint with a unique transaction identifier to get a single transaction for an authenticated customer."
					},
					"response": [
						{
							"name": "Get Transaction",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "x-access-token",
										"value": "{{x_access_token}}",
										"type": "text"
									}
								],
								"url": {
									"raw": "{{base_url}}kolo/transactions/:id",
									"host": [
										"{{base_url}}kolo"
									],
									"path": [
										"transactions",
										":id"
									],
									"variable": [
										{
											"key": "id",
											"value": "c954f391-83a6-4265-bf7a-e9e1d2db5013"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "X-Powered-By",
									"value": "Express"
								},
								{
									"key": "X-Request-ID",
									"value": "c99e9563-43ea-4ed1-bc17-389ace9bf87c"
								},
								{
									"key": "Last-Modified",
									"value": "Thu, 20 Jun 2024 14:16:34 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json; charset=utf-8"
								},
								{
									"key": "Content-Length",
									"value": "981"
								},
								{
									"key": "ETag",
									"value": "W/\"3d5-NGVm4vZe4JS0ue7xFxrWIWwsjx4\""
								},
								{
									"key": "Date",
									"value": "Thu, 20 Jun 2024 14:16:38 GMT"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Keep-Alive",
									"value": "timeout=5"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"success\",\n    \"data\": {\n        \"id\": \"c954f391-83a6-4265-bf7a-e9e1d2db5013\",\n        \"account_number\": \"2208667061\",\n        \"currency\": \"NGN\",\n        \"amount\": \"10.00\",\n        \"balance\": \"436.56\",\n        \"reference\": \"\",\n        \"hash\": \"{\\\"account_number\\\":\\\"2208667061\\\",\\\"bank_code\\\":\\\"057\\\",\\\"amount\\\":10,\\\"balance\\\":436,\\\"type\\\":\\\"credit\\\",\\\"date\\\":\\\"2024-06-08T15:03:00Z\\\"}\",\n        \"status\": \"success\",\n        \"entry_type\": \"credit\",\n        \"narration\": \"NIP/ROLEZ/Transfer/Transfer to Adewunmi O Akinsanya/***7/AT5_MFDS110202406081601\",\n        \"transaction_date\": \"2024-06-08T15:02:10.000Z\",\n        \"transaction_type\": \"Credit\",\n        \"note\": null,\n        \"source\": \"email\",\n        \"provider\": \"google\",\n        \"categories\": [],\n        \"bank\": {\n            \"id\": \"d645920e395fedad7bbbed0eca3fe2e0\",\n            \"name\": \"Zenith Bank\",\n            \"short_code\": \"057\",\n            \"long_code\": \"057\",\n            \"icon\": \"https://s3.us-east-2.amazonaws.com/kolo.finance/assets/zenithbank-logo-circle.png\"\n        },\n        \"created_on\": \"2024-06-14T19:00:07.070Z\",\n        \"created_by\": null,\n        \"modified_on\": \"2024-06-14T19:00:07.000Z\",\n        \"modified_by\": null,\n        \"deleted_on\": null,\n        \"deleted_by\": null\n    },\n    \"meta\": {\n        \"cost\": 0,\n        \"balance\": 585\n    }\n}"
						}
					]
				},
				{
					"name": "Update Transaction",
					"request": {
						"method": "PATCH",
						"header": [
							{
								"key": "x-access-token",
								"value": "{{x_access_token}}",
								"type": "text"
							}
						],
						"body": {
							"mode": "raw",
							"raw": "{\n    \"note\": \"Updated by API\"\n}",
							"options": {
								"raw": {
									"language": "json"
								}
							}
						},
						"url": {
							"raw": "{{base_url}}kolo/transactions/:id",
							"host": [
								"{{base_url}}kolo"
							],
							"path": [
								"transactions",
								":id"
							],
							"variable": [
								{
									"key": "id",
									"value": "c954f391-83a6-4265-bf7a-e9e1d2db5013"
								}
							]
						},
						"description": "Use this endpoint to update the details of a transaction using the unique identifier of the transaction."
					},
					"response": []
				},
				{
					"name": "List Bank Accounts",
					"request": {
						"method": "GET",
						"header": [
							{
								"key": "x-access-token",
								"value": "{{x_access_token}}",
								"type": "text"
							}
						],
						"url": {
							"raw": "{{base_url}}kolo/bank-accounts",
							"host": [
								"{{base_url}}kolo"
							],
							"path": [
								"bank-accounts"
							]
						},
						"description": "Use this endpoint to get all the bank accounts of an authenticated user."
					},
					"response": [
						{
							"name": "List Bank Accounts",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "x-access-token",
										"value": "{{x_access_token}}",
										"type": "text"
									}
								],
								"url": {
									"raw": "{{base_url}}kolo/bank-accounts",
									"host": [
										"{{base_url}}kolo"
									],
									"path": [
										"bank-accounts"
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "X-Powered-By",
									"value": "Express"
								},
								{
									"key": "X-Request-ID",
									"value": "a87040a9-22aa-4e18-808e-7945a6c62754"
								},
								{
									"key": "Last-Modified",
									"value": "Thu, 20 Jun 2024 14:17:21 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json; charset=utf-8"
								},
								{
									"key": "Content-Length",
									"value": "714"
								},
								{
									"key": "ETag",
									"value": "W/\"2ca-gPZE9AF1kgKZM+GHN3nVUwxuLd8\""
								},
								{
									"key": "Date",
									"value": "Thu, 20 Jun 2024 14:17:23 GMT"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Keep-Alive",
									"value": "timeout=5"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"success\",\n    \"data\": [\n        {\n            \"id\": \"6412961b-bf28-4096-9391-6dc899ab3032\",\n            \"account_name\": \"Adewunmi O Akinsanya\",\n            \"account_number\": \"2208667061\",\n            \"balance\": \"436.56\",\n            \"currency\": \"NGN\",\n            \"last_balance_time\": \"2024-06-08T15:02:10.000Z\",\n            \"last_synced\": \"2024-06-14T19:00:07.000Z\",\n            \"data_source\": [\n                \"email\"\n            ],\n            \"description\": \"Autodiscovered by Kolo\",\n            \"bank\": {\n                \"id\": \"d645920e395fedad7bbbed0eca3fe2e0\",\n                \"name\": \"Zenith Bank\",\n                \"short_code\": \"057\",\n                \"long_code\": \"057\",\n                \"icon\": \"https://s3.us-east-2.amazonaws.com/kolo.finance/assets/zenithbank-logo-circle.png\"\n            },\n            \"created_on\": \"2024-04-12T13:29:31.782Z\",\n            \"created_by\": null,\n            \"modified_on\": \"2024-06-14T19:00:07.000Z\",\n            \"modified_by\": null,\n            \"deleted_on\": null,\n            \"deleted_by\": null\n        }\n    ],\n    \"meta\": {\n        \"cost\": 0,\n        \"balance\": 585\n    }\n}"
						}
					]
				},
				{
					"name": "Get Bank Account",
					"request": {
						"method": "GET",
						"header": [
							{
								"key": "x-access-token",
								"value": "{{x_access_token}}",
								"type": "text"
							}
						],
						"url": {
							"raw": "{{base_url}}kolo/bank-accounts/:id",
							"host": [
								"{{base_url}}kolo"
							],
							"path": [
								"bank-accounts",
								":id"
							],
							"variable": [
								{
									"key": "id",
									"value": "6412961b-bf28-4096-9391-6dc899ab3032"
								}
							]
						},
						"description": "Use this endpoint to get a specific bank account of an authenticated user using the unique identifier of the bank account."
					},
					"response": [
						{
							"name": "Get Bank Account",
							"originalRequest": {
								"method": "GET",
								"header": [
									{
										"key": "x-access-token",
										"value": "{{x_access_token}}",
										"type": "text"
									}
								],
								"url": {
									"raw": "{{base_url}}kolo/bank-accounts/:id",
									"host": [
										"{{base_url}}kolo"
									],
									"path": [
										"bank-accounts",
										":id"
									],
									"variable": [
										{
											"key": "id",
											"value": "6412961b-bf28-4096-9391-6dc899ab3032"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "X-Powered-By",
									"value": "Express"
								},
								{
									"key": "X-Request-ID",
									"value": "edeb094b-8a91-4e1b-8053-a90a763bcc37"
								},
								{
									"key": "Last-Modified",
									"value": "Thu, 20 Jun 2024 14:18:05 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json; charset=utf-8"
								},
								{
									"key": "Content-Length",
									"value": "712"
								},
								{
									"key": "ETag",
									"value": "W/\"2c8-gZIC1IX58/OqVd6iXQOmoXUiCxg\""
								},
								{
									"key": "Date",
									"value": "Thu, 20 Jun 2024 14:18:09 GMT"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Keep-Alive",
									"value": "timeout=5"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"success\",\n    \"data\": {\n        \"id\": \"6412961b-bf28-4096-9391-6dc899ab3032\",\n        \"account_name\": \"Adewunmi O Akinsanya\",\n        \"account_number\": \"2208667061\",\n        \"balance\": \"436.56\",\n        \"currency\": \"NGN\",\n        \"last_balance_time\": \"2024-06-08T15:02:10.000Z\",\n        \"last_synced\": \"2024-06-14T19:00:07.000Z\",\n        \"data_source\": [\n            \"email\"\n        ],\n        \"description\": \"Autodiscovered by Kolo\",\n        \"bank\": {\n            \"id\": \"d645920e395fedad7bbbed0eca3fe2e0\",\n            \"name\": \"Zenith Bank\",\n            \"short_code\": \"057\",\n            \"long_code\": \"057\",\n            \"icon\": \"https://s3.us-east-2.amazonaws.com/kolo.finance/assets/zenithbank-logo-circle.png\"\n        },\n        \"created_on\": \"2024-04-12T13:29:31.782Z\",\n        \"created_by\": null,\n        \"modified_on\": \"2024-06-14T19:00:07.000Z\",\n        \"modified_by\": null,\n        \"deleted_on\": null,\n        \"deleted_by\": null\n    },\n    \"meta\": {\n        \"cost\": 0,\n        \"balance\": 585\n    }\n}"
						}
					]
				},
				{
					"name": "Get Profile",
					"request": {
						"method": "GET",
						"header": [
							{
								"key": "x-access-token",
								"value": "{{x_access_token}}",
								"type": "text"
							}
						],
						"url": {
							"raw": "{{base_url}}kolo/profile",
							"host": [
								"{{base_url}}kolo"
							],
							"path": [
								"profile"
							]
						},
						"description": "Use this endpoint to retrieve the profile information of an authenticated user."
					},
					"response": []
				},
				{
					"name": "Add Bank Account",
					"request": {
						"method": "POST",
						"header": [
							{
								"key": "x-access-token",
								"value": "{{x_access_token}}",
								"type": "text"
							}
						],
						"body": {
							"mode": "raw",
							"raw": "{\n    \"bank_id\": null,\n    \"description\": \"\",\n    \"account_number\": \"\",\n    \"data_source\": [\"email\", \"sms\", \"bank\"],\n    \"currency\": \"NGN\"\n}",
							"options": {
								"raw": {
									"language": "json"
								}
							}
						},
						"url": {
							"raw": "{{base_url}}kolo/bank-accounts",
							"host": [
								"{{base_url}}kolo"
							],
							"path": [
								"bank-accounts"
							]
						},
						"description": "Use this endpoint to add a new bank account for an authenticated user."
					},
					"response": []
				},
				{
					"name": "Sync Bank Account",
					"request": {
						"method": "POST",
						"header": [
							{
								"key": "x-access-token",
								"value": "{{x_access_token}}",
								"type": "text"
							}
						],
						"url": {
							"raw": "{{base_url}}kolo/bank-accounts/sync",
							"host": [
								"{{base_url}}kolo"
							],
							"path": [
								"bank-accounts",
								"sync"
							]
						},
						"description": "Use this endpoint to sync a bank account to update its information. To do this, you will need the unique identifier of the the bank account."
					},
					"response": []
				},
				{
					"name": "Update Bank Account",
					"request": {
						"method": "PATCH",
						"header": [
							{
								"key": "x-access-token",
								"value": "{{x_access_token}}",
								"type": "text"
							}
						],
						"body": {
							"mode": "raw",
							"raw": "{\n    \"description\": \"Testing\",\n    \"account_number\": \"2208667061\",\n    \"data_source\": [\n        \"email\",\n        \"sms\",\n        \"bank\"\n    ]\n}",
							"options": {
								"raw": {
									"language": "json"
								}
							}
						},
						"url": {
							"raw": "{{base_url}}kolo/bank-accounts/:id",
							"host": [
								"{{base_url}}kolo"
							],
							"path": [
								"bank-accounts",
								":id"
							],
							"variable": [
								{
									"key": "id",
									"value": "6412961b-bf28-4096-9391-6dc899ab3032"
								}
							]
						},
						"description": "Use this endpoint to update the bank account of an authenticated user using it's unique identifier."
					},
					"response": [
						{
							"name": "Update Bank Account",
							"originalRequest": {
								"method": "PATCH",
								"header": [
									{
										"key": "x-access-token",
										"value": "{{x_access_token}}",
										"type": "text"
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\n    \"description\": \"Testing\",\n    \"account_number\": \"2208667061\",\n    \"data_source\": [\n        \"email\",\n        \"sms\",\n        \"bank\"\n    ]\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}kolo/bank-accounts/:id",
									"host": [
										"{{base_url}}kolo"
									],
									"path": [
										"bank-accounts",
										":id"
									],
									"variable": [
										{
											"key": "id",
											"value": "6412961b-bf28-4096-9391-6dc899ab3032"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "X-Powered-By",
									"value": "Express"
								},
								{
									"key": "X-Request-ID",
									"value": "c7bea6c7-1255-4f5f-8584-18004771e81d"
								},
								{
									"key": "Last-Modified",
									"value": "Thu, 20 Jun 2024 14:27:35 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json; charset=utf-8"
								},
								{
									"key": "Content-Length",
									"value": "512"
								},
								{
									"key": "ETag",
									"value": "W/\"200-UhBtZqvLbr0i7NBAEYKUWtbSmFg\""
								},
								{
									"key": "Date",
									"value": "Thu, 20 Jun 2024 14:27:38 GMT"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Keep-Alive",
									"value": "timeout=5"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"success\",\n    \"data\": {\n        \"id\": \"6412961b-bf28-4096-9391-6dc899ab3032\",\n        \"account_name\": \"Adewunmi O Akinsanya\",\n        \"account_number\": \"2208667061\",\n        \"balance\": \"436.56\",\n        \"currency\": \"NGN\",\n        \"last_balance_time\": \"2024-06-08T15:02:10.000Z\",\n        \"last_synced\": \"2024-06-14T19:00:07.000Z\",\n        \"data_source\": [\n            \"email\",\n            \"sms\",\n            \"bank\"\n        ],\n        \"description\": \"Testing\",\n        \"created_on\": \"2024-04-12T13:29:31.782Z\",\n        \"created_by\": null,\n        \"modified_on\": \"2024-06-14T19:00:07.000Z\",\n        \"modified_by\": null,\n        \"deleted_on\": null,\n        \"deleted_by\": null\n    },\n    \"meta\": {\n        \"cost\": 0,\n        \"balance\": 585\n    }\n}"
						}
					]
				},
				{
					"name": "Delete Bank Account",
					"request": {
						"method": "DELETE",
						"header": [
							{
								"key": "x-access-token",
								"value": "{{x_access_token}}",
								"type": "text"
							}
						],
						"url": {
							"raw": "{{base_url}}kolo/bank-accounts/:id",
							"host": [
								"{{base_url}}kolo"
							],
							"path": [
								"bank-accounts",
								":id"
							],
							"variable": [
								{
									"key": "id",
									"value": "6412961b-bf28-4096-9391-6dc899ab3032"
								}
							]
						},
						"description": "Use this endpoint to delete a specific bank account from the user's profile."
					},
					"response": [
						{
							"name": "Delete Bank Account",
							"originalRequest": {
								"method": "DELETE",
								"header": [
									{
										"key": "x-access-token",
										"value": "{{x_access_token}}",
										"type": "text"
									}
								],
								"url": {
									"raw": "{{base_url}}kolo/bank-accounts/:id",
									"host": [
										"{{base_url}}kolo"
									],
									"path": [
										"bank-accounts",
										":id"
									],
									"variable": [
										{
											"key": "id",
											"value": "6412961b-bf28-4096-9391-6dc899ab3032"
										}
									]
								}
							},
							"status": "OK",
							"code": 200,
							"_postman_previewlanguage": "json",
							"header": [
								{
									"key": "X-Powered-By",
									"value": "Express"
								},
								{
									"key": "X-Request-ID",
									"value": "76becb60-b7e8-448e-aada-962864fb628a"
								},
								{
									"key": "Last-Modified",
									"value": "Thu, 20 Jun 2024 14:27:59 GMT"
								},
								{
									"key": "Content-Type",
									"value": "application/json; charset=utf-8"
								},
								{
									"key": "Content-Length",
									"value": "62"
								},
								{
									"key": "ETag",
									"value": "W/\"3e-az9L1kBMghnzvIrHYAC/QjGUpBw\""
								},
								{
									"key": "Date",
									"value": "Thu, 20 Jun 2024 14:28:03 GMT"
								},
								{
									"key": "Connection",
									"value": "keep-alive"
								},
								{
									"key": "Keep-Alive",
									"value": "timeout=5"
								}
							],
							"cookie": [],
							"body": "{\n    \"status\": \"success\",\n    \"data\": {},\n    \"meta\": {\n        \"cost\": 0,\n        \"balance\": 585\n    }\n}"
						}
					]
				}
			],
			"description": "> Kolo transactional data is still in beta consequently, a few things may not work as expected. If you encounter any bugs, please email support@lendsqr.com. \n  \n\n### Introduction\n\n[Kolo](https://lsq.li/kolo?s=documentation) is a financial management application that consolidates all your bank accounts into a single platform. With Kolo, users can view balances, transactions, categorize spending, and much more. Our API extends these functionalities, allowing developers to integrate Kolo’s features into their applications. This API enables the tracking of bank balances and transactions, giving you a glimpse of your customers financial health.\n\n### Getting Started\n\nTo use the Kolo API, customers need to:\n\n1. **Create an Account**: Users must sign up for an account with [Kolo](https://lsq.li/kolo-app?s=documentation).\n    \n2. **Grant Permissions**: Users need to authorize the API to access their bank account information.\n    \n\n### Authentication\n\nThe Kolo API uses OAuth 2.0 for authentication. Ensure that you have valid credentials and have completed the necessary authorization steps to interact with the endpoints."
		},
		{
			"name": "Core Services",
			"item": [
				{
					"name": "Auth",
					"item": [
						{
							"name": "Auth",
							"request": {
								"method": "POST",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\r\n  \"email\": \"api@example.com\",\r\n    \"password\": \"Test123##\"\r\n}\r\n",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}customers/auth",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										"auth"
									]
								},
								"description": "Authenticate a user by invoking the Auth endpoint to generate the `x-access-token`. This token is derived from the user's email and password and is mandatory for accessing all secured endpoints within the core services.\n\n#### Request Payload\n\n| Property | Type | Examples |\n| --- | --- | --- |\n| `email` | `string` | [api@example.com](https://mailto:api@example.com) |\n| `password` | `string` | Test123## |"
							},
							"response": [
								{
									"name": "Auth",
									"originalRequest": {
										"method": "POST",
										"header": [],
										"body": {
											"mode": "raw",
											"raw": "{\r\n  \"email\": \"api@example.com\",\r\n    \"password\": \"Test123##\"\r\n}\r\n",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{base_url}}customers/auth",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												"auth"
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": "{\r\n    \"token\": \"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NzI5OSwiaXNfYWRtaW4iOnRydWUsImlwIjoiMy4yMi41NS4xMDUiLCJyb2xlIjp7Im5hbWUiOiJTdXBlciBBZG1pbiIsInNsdWciOiJzdXBlcl9hZG1pbiJ9LCJjdXJ0eXBlX2lkIjoyLCJ0eXBlIjoibGVuZGVyIiwibmFtZSI6ImxlbmRlcmNvIiwicHJpbWFyeV9lbWFpbCI6InRoZXJlc2FAbGVuZHNxci5jb20iLCJzdXBwb3J0X2VtYWlsIjoidGhlcmVzYUBsZW5kc3FyLmNvbSIsImxvZ29fdXJsIjoiaHR0cHM6Ly9kb2N1bWVudHMubGVuZHNxci5jb20vZGVmYXVsdC8xODI1ZGI1M\"\r\n}"
								}
							]
						}
					],
					"description": "The APIs in this folder are specifically designed to handle authentication operations, including the generation and management of tokens required for secure access to other core service APIs.\n\n#### Auth Endpoint Functionality\n\nThe Auth endpoint is responsible for issuing the `x-access-token`, a critical component for accessing APIs within the core services collection. This token must be used in conjunction with the Bearer token to authorize subsequent API requests.\n\n#### Making Auth API Calls\n\nWhen invoking the Auth endpoint, ensure that the Bearer token is included in the request headers to authenticate the call. This token acts as your application's API key and is mandatory for successfully obtaining the `x-access-token`.",
					"event": [
						{
							"listen": "prerequest",
							"script": {
								"type": "text/javascript",
								"exec": [
									""
								]
							}
						},
						{
							"listen": "test",
							"script": {
								"type": "text/javascript",
								"packages": {},
								"exec": [
									""
								]
							}
						}
					]
				},
				{
					"name": "Customers",
					"item": [
						{
							"name": "Create new Customer",
							"request": {
								"method": "POST",
								"header": [
									{
										"key": "Cache-Control",
										"value": "no-cache",
										"type": "text"
									},
									{
										"key": "Postman-Token",
										"value": "<calculated when request is sent>",
										"type": "text"
									},
									{
										"key": "Content-Type",
										"value": "application/json",
										"type": "text"
									},
									{
										"key": "Content-Length",
										"value": "<calculated when request is sent>",
										"type": "text"
									},
									{
										"key": "Host",
										"value": "<calculated when request is sent>",
										"type": "text"
									},
									{
										"key": "User-Agent",
										"value": "PostmanRuntime/7.39.1",
										"type": "text"
									},
									{
										"key": "Accept",
										"value": "*/*",
										"type": "text"
									},
									{
										"key": "Accept-Encoding",
										"value": "gzip, deflate, br",
										"type": "text"
									},
									{
										"key": "Connection",
										"value": "keep-alive",
										"type": "text"
									},
									{
										"key": "x-access-token",
										"value": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NTMyLCJpc19hZG1pbiI6dHJ1ZSwiaXAiOiIxMDUuMTEzLjEwOC4xNzAiLCJyb2xlIjp7Im5hbWUiOiJTdXBlciBBZG1pbiIsInNsdWciOiJzdXBlcl9hZG1pbiJ9LCJjdXJyZW50X29yZ2FuaXphdGlvbiI6eyJpZCI6MjA3LCJzbHVnIjoicWFsb2FucyIsInR5cGVfaWQiOjIsInR5cGUiOiJsZW5kZXIiLCJuYW1lIjoiUUFsb2FucyIsInByaW1hcnlfZW1haWwiOiJzYW11ZWxAbGVuZHNxci5jb20iLCJzdXBwb3J0X2VtYWlsIjoic2FtdWVsQGxlbmRzcXIuY29tIiwibG9nb191cmwiOiJodHRwczovL2FwcC5sZW5kc3FyLmNvbS9hc3NldHMvbG9nby5zdmciLCJ0aWVyIjowLCJzdGF0dXMiOm51bGwsImNvdW50cnkiOiJOR0EiLCJjdXJyZW5jeSI6Ik5HTiJ9LCJyZWdpb24iOiJMYWdvcyIsInNlc3Npb25faWQiOiIyMDI0MDcyMjE1MzcxOS0wMDIwNy1BRDUzMi1MU1EtVngwbTdFR3FMRiIsImlhdCI6MTcyMTY2MjYzOSwiZXhwIjoxNzIxNjY2MjM5LCJpc3MiOiJsZW5kc3FyLmNvbSJ9.uS5piy01tjwf8AzvKfaQ3vXW621-NDsd_-ZblXZPxVg",
										"type": "text",
										"disabled": true
									}
								],
								"body": {
									"mode": "raw",
									"raw": "{\r\n  \"phone_number\": \"07123456789\",\r\n  \"bvn\": \"\",\r\n  \"bvn_phone_number\": \"07123456789\",\r\n  \"dob\": \"1999-11-11\",\r\n  \"email\": \"\",\r\n  \"account_number\": \"\",\r\n  \"bank_code\": \"\",  \r\n  \"state\": \"\",\r\n  \"lga\": \"\",\r\n  \"city\": \"Test City\",\r\n  \"address\": \"123 Test St\",\r\n  \"photo_url\": \"http://example.com/photo.jpg\",\r\n  \"documents\": [\r\n    {\r\n      \"url\": \"http://example.com/document1.pdf\",\r\n      \"type_id\": 1,\r\n      \"sub_type_id\": 2\r\n    },\r\n    {\r\n      \"url\": \"http://example.com/document2.pdf\",\r\n      \"type_id\": 3,\r\n      \"sub_type_id\": 4\r\n    }\r\n  ]\r\n}\r\n",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}customers",
									"host": [
										"{{base_url}}customers"
									]
								},
								"description": "Create a new customer with the provided details, including phone number, BVN, email, address, and associated documents.\n\n#### Request Payload\n\n| Property | Type | Description |\n| --- | --- | --- |\n| `phone_number` | `string` | **Required.** The phone number of the customer. The number should be in the form `08012345678`. |\n| `bvn` | `string` | **Required.** This is the Bank Verification Number (BVN) of the customer. |\n| `bvn_phone_number` | `string` | **Required.** This is the phone number attached to their BVN.  <br>  <br>Please provide the correct number as there is a validation check on the BVN and this phone number. |\n| `dob` | `string` | **Required.** Date of birth in the format `YYYY-MM-DD`.  <br>  <br>Ensure the date provided here matches the date on their BVN. |\n| `email` | `string` | **Required.** Email address of the customer. |\n| `account_number` | `string` | **Required.** The account number of the customer. |\n| `bank_code` | `string` | **Required.** The bank code of the account number added in order to identify the customer's bank. |\n| `state_id` | `string` | **Optional.** ID of the state the customer resides.  <br>  <br>This is optional if the `state` is known. |\n| `state` | `string` | **Optional.** Name of the state the customer resides.  <br>  <br>This is optional if the `state_id` is known. |\n| `lga_id` | `string` | **Required.** ID of the local government area the customer resides. |\n| `lga` | `string` | **Optional.** Name of the lga inside the state the customer resides.  <br>  <br>This is optional if the lga`_id` is known. |\n| `city` | `string` | **Required.** Name of the city the customer resides. |\n| `address` | `string` | **Required.** Address of the customer. |\n| `photo_url` | `string` | **Optional.** URL to the customer's photo. |\n| `documents` | `array` | **Optional.** Array of documents associated with the customer. Each document should have `url`, `type_id`, and `sub_type_id`. |"
							},
							"response": [
								{
									"name": "Create new Customer",
									"originalRequest": {
										"method": "POST",
										"header": [
											{
												"key": "Cache-Control",
												"value": "no-cache",
												"type": "text"
											},
											{
												"key": "Postman-Token",
												"value": "<calculated when request is sent>",
												"type": "text"
											},
											{
												"key": "Content-Type",
												"value": "application/json",
												"type": "text"
											},
											{
												"key": "Content-Length",
												"value": "<calculated when request is sent>",
												"type": "text"
											},
											{
												"key": "Host",
												"value": "<calculated when request is sent>",
												"type": "text"
											},
											{
												"key": "User-Agent",
												"value": "PostmanRuntime/7.39.1",
												"type": "text"
											},
											{
												"key": "Accept",
												"value": "*/*",
												"type": "text"
											},
											{
												"key": "Accept-Encoding",
												"value": "gzip, deflate, br",
												"type": "text"
											},
											{
												"key": "Connection",
												"value": "keep-alive",
												"type": "text"
											},
											{
												"key": "x-access-token",
												"value": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NTMyLCJpc19hZG1pbiI6dHJ1ZSwiaXAiOiIxMDUuMTEzLjEwOC4xNzAiLCJyb2xlIjp7Im5hbWUiOiJTdXBlciBBZG1pbiIsInNsdWciOiJzdXBlcl9hZG1pbiJ9LCJjdXJyZW50X29yZ2FuaXphdGlvbiI6eyJpZCI6MjA3LCJzbHVnIjoicWFsb2FucyIsInR5cGVfaWQiOjIsInR5cGUiOiJsZW5kZXIiLCJuYW1lIjoiUUFsb2FucyIsInByaW1hcnlfZW1haWwiOiJzYW11ZWxAbGVuZHNxci5jb20iLCJzdXBwb3J0X2VtYWlsIjoic2FtdWVsQGxlbmRzcXIuY29tIiwibG9nb191cmwiOiJodHRwczovL2FwcC5sZW5kc3FyLmNvbS9hc3NldHMvbG9nby5zdmciLCJ0aWVyIjowLCJzdGF0dXMiOm51bGwsImNvdW50cnkiOiJOR0EiLCJjdXJyZW5jeSI6Ik5HTiJ9LCJyZWdpb24iOiJMYWdvcyIsInNlc3Npb25faWQiOiIyMDI0MDcyMjE1MzcxOS0wMDIwNy1BRDUzMi1MU1EtVngwbTdFR3FMRiIsImlhdCI6MTcyMTY2MjYzOSwiZXhwIjoxNzIxNjY2MjM5LCJpc3MiOiJsZW5kc3FyLmNvbSJ9.uS5piy01tjwf8AzvKfaQ3vXW621-NDsd_-ZblXZPxVg",
												"type": "text",
												"disabled": true
											}
										],
										"body": {
											"mode": "raw",
											"raw": "{\r\n  \"phone_number\": \"07123456789\",\r\n  \"bvn\": \"\",\r\n  \"bvn_phone_number\": \"07123456789\",\r\n  \"dob\": \"1999-11-11\",\r\n  \"email\": \"\",\r\n  \"account_number\": \"\",\r\n  \"bank_code\": \"\",  \r\n  \"state\": \"\",\r\n  \"lga\": \"\",\r\n  \"city\": \"Test City\",\r\n  \"address\": \"123 Test St\",\r\n  \"photo_url\": \"http://example.com/photo.jpg\",\r\n  \"documents\": [\r\n    {\r\n      \"url\": \"http://example.com/document1.pdf\",\r\n      \"type_id\": 1,\r\n      \"sub_type_id\": 2\r\n    },\r\n    {\r\n      \"url\": \"http://example.com/document2.pdf\",\r\n      \"type_id\": 3,\r\n      \"sub_type_id\": 4\r\n    }\r\n  ]\r\n}\r\n",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{base_url}}customers",
											"host": [
												"{{base_url}}customers"
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": "{\r\n    \"status\": \"success\",\r\n    \"message\": \"Successful\",\r\n    \"data\": {\r\n        \"users\": [\r\n            {\r\n                \"id\": 00008999,\r\n                \"org_id\": 340015,\r\n                \"manager_id\": null,\r\n                \"office_id\": null,\r\n                \"first_name\": \"First\",\r\n                \"last_name\": \"User\",\r\n                \"phone_number\": \"23480123456789\",\r\n                \"country\": \"NGA\",\r\n                \"language\": \"en\",\r\n                \"locale\": \"en-US\",\r\n                \"timezone\": \"Africa/Lagos\",\r\n                \"email\": \"exampleuser@gmail.com\",\r\n                \"email_verified\": 0,\r\n                \"bvn\": \"22*******98\",\r\n                \"id_document_id\": null,\r\n                \"bvn_phone_number\": \"08169654518\",\r\n                \"bvn_validation_count\": 0,\r\n                \"dob\": \"1995-07-15T00:00:00.000Z\",\r\n                \"charged_for_id_verification\": 1,\r\n                \"photo_url\": \"https://documents.example.png\",\r\n                \"address\": null,\r\n                \"apartment_type\": null,\r\n                \"nearest_landmark\": null,\r\n                \"city\": null,\r\n                \"state\": \"Kaduna State\",\r\n                \"lga\": null,\r\n                \"gender\": \"Male\",\r\n                \"marital_status\": null,\r\n                \"rating\": null,\r\n                \"credit_score\": null,\r\n                \"risk_rating\": null,\r\n                \"selfie_bvn_check\": \"Successful\",\r\n                \"selfie_id_check\": null,\r\n                \"referred_by\": null,\r\n                \"referral_code\": \"EP4N9A\",\r\n                \"activated\": 1,\r\n                \"activated_on\": null,\r\n                \"last_login_date\": \"2024-08-10T23:07:48.000Z\",\r\n                \"blacklisted\": 0,\r\n                \"reason\": null,\r\n                \"created_on\": \"2024-08-10T23:07:48.000Z\"\r\n            }\r\n            \r\n        ]\r\n    },\r\n    \"meta\": {\r\n        \"cost\": 100,\r\n        \"balance\": 1555\r\n    }\r\n}"
								}
							]
						},
						{
							"name": "Activate Customer",
							"request": {
								"method": "PUT",
								"header": [],
								"url": {
									"raw": "{{base_url}}customers/:id/activate",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										":id",
										"activate"
									],
									"variable": [
										{
											"key": "id",
											"value": ""
										}
									]
								},
								"description": "Activate a customer with their unique ID after creation to enable access to loan functionalities and other associated actions.\n\n> This should be called immediately after the customer is created."
							},
							"response": [
								{
									"name": "Activate Customer",
									"originalRequest": {
										"method": "PUT",
										"header": [],
										"url": {
											"raw": "{{base_url}}customers/:id/activate",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												":id",
												"activate"
											],
											"variable": [
												{
													"key": "id",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						},
						{
							"name": "Get  All Customers",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}customers",
									"host": [
										"{{base_url}}customers"
									]
								},
								"description": "Retrieve a list of all customers. This endpoint returns comprehensive customer data, which can be filtered or paginated as required."
							},
							"response": [
								{
									"name": "Get  All Customers",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}customers",
											"host": [
												"{{base_url}}customers"
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": "{\r\n    \"status\": \"success\",\r\n    \"message\": \"Successful\",\r\n    \"data\": {\r\n        \"users\": [\r\n            {\r\n                \"id\": 00008999,\r\n                \"org_id\": 340015,\r\n                \"manager_id\": null,\r\n                \"office_id\": null,\r\n                \"first_name\": \"First\",\r\n                \"last_name\": \"User\",\r\n                \"phone_number\": \"23480123456789\",\r\n                \"country\": \"NGA\",\r\n                \"language\": \"en\",\r\n                \"locale\": \"en-US\",\r\n                \"timezone\": \"Africa/Lagos\",\r\n                \"email\": \"exampleuser@gmail.com\",\r\n                \"email_verified\": 0,\r\n                \"bvn\": \"22*******98\",\r\n                \"id_document_id\": null,\r\n                \"bvn_phone_number\": \"08169654518\",\r\n                \"bvn_validation_count\": 0,\r\n                \"dob\": \"1995-07-15T00:00:00.000Z\",\r\n                \"charged_for_id_verification\": 1,\r\n                \"photo_url\": \"https://documents.example.png\",\r\n                \"address\": null,\r\n                \"apartment_type\": null,\r\n                \"nearest_landmark\": null,\r\n                \"city\": null,\r\n                \"state\": \"Kaduna State\",\r\n                \"lga\": null,\r\n                \"gender\": \"Male\",\r\n                \"marital_status\": null,\r\n                \"rating\": null,\r\n                \"credit_score\": null,\r\n                \"risk_rating\": null,\r\n                \"selfie_bvn_check\": \"Successful\",\r\n                \"selfie_id_check\": null,\r\n                \"referred_by\": null,\r\n                \"referral_code\": \"EP4N9A\",\r\n                \"activated\": 1,\r\n                \"activated_on\": null,\r\n                \"last_login_date\": \"2024-08-10T23:07:48.000Z\",\r\n                \"blacklisted\": 0,\r\n                \"reason\": null,\r\n                \"created_on\": \"2024-08-10T23:07:48.000Z\"\r\n            },\r\n            {\r\n                \"id\": 00008999,\r\n                \"org_id\": 340015,\r\n                \"manager_id\": null,\r\n                \"office_id\": null,\r\n                \"first_name\": \"First\",\r\n                \"last_name\": \"User\",\r\n                \"phone_number\": \"23480123456789\",\r\n                \"country\": \"NGA\",\r\n                \"language\": \"en\",\r\n                \"locale\": \"en-US\",\r\n                \"timezone\": \"Africa/Lagos\",\r\n                \"email\": \"exampleuser@gmail.com\",\r\n                \"email_verified\": 0,\r\n                \"bvn\": \"22*******98\",\r\n                \"id_document_id\": null,\r\n                \"bvn_phone_number\": \"08169654518\",\r\n                \"bvn_validation_count\": 0,\r\n                \"dob\": \"1995-07-15T00:00:00.000Z\",\r\n                \"charged_for_id_verification\": 1,\r\n                \"photo_url\": \"https://documents.example.png\",\r\n                \"address\": null,\r\n                \"apartment_type\": null,\r\n                \"nearest_landmark\": null,\r\n                \"city\": null,\r\n                \"state\": \"Kaduna State\",\r\n                \"lga\": null,\r\n                \"gender\": \"Male\",\r\n                \"marital_status\": null,\r\n                \"rating\": null,\r\n                \"credit_score\": null,\r\n                \"risk_rating\": null,\r\n                \"selfie_bvn_check\": \"Successful\",\r\n                \"selfie_id_check\": null,\r\n                \"referred_by\": null,\r\n                \"referral_code\": \"EP4N9A\",\r\n                \"activated\": 1,\r\n                \"activated_on\": null,\r\n                \"last_login_date\": \"2024-08-10T23:07:48.000Z\",\r\n                \"blacklisted\": 0,\r\n                \"reason\": null,\r\n                \"created_on\": \"2024-08-10T23:07:48.000Z\"\r\n            },\r\n            ...\r\n            \r\n        ]\r\n    },\r\n    \"meta\": {\r\n        \"cost\": 100,\r\n        \"balance\": 1555\r\n    }\r\n}"
								}
							]
						},
						{
							"name": "Get Single Customer",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}customers/:id",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										":id"
									],
									"variable": [
										{
											"key": "id",
											"value": ""
										}
									]
								},
								"description": "Retrieve detailed information for a single customer by their unique ID."
							},
							"response": [
								{
									"name": "Get Single Customer",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}customers/:id",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												":id"
											],
											"variable": [
												{
													"key": "id",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": [],
									"cookie": [
										{
											"expires": "Invalid Date",
											"domain": "",
											"path": ""
										}
									],
									"body": "{\r\n    \"status\": \"success\",\r\n    \"message\": \"Successful\",\r\n    \"data\": {\r\n        \"users\": [\r\n            {\r\n                \"id\": 00008999,\r\n                \"org_id\": 340015,\r\n                \"manager_id\": null,\r\n                \"office_id\": null,\r\n                \"first_name\": \"First\",\r\n                \"last_name\": \"User\",\r\n                \"phone_number\": \"23480123456789\",\r\n                \"country\": \"NGA\",\r\n                \"language\": \"en\",\r\n                \"locale\": \"en-US\",\r\n                \"timezone\": \"Africa/Lagos\",\r\n                \"email\": \"exampleuser@gmail.com\",\r\n                \"email_verified\": 0,\r\n                \"bvn\": \"22*******98\",\r\n                \"id_document_id\": null,\r\n                \"bvn_phone_number\": \"08169654518\",\r\n                \"bvn_validation_count\": 0,\r\n                \"dob\": \"1995-07-15T00:00:00.000Z\",\r\n                \"charged_for_id_verification\": 1,\r\n                \"photo_url\": \"https://documents.example.png\",\r\n                \"address\": null,\r\n                \"apartment_type\": null,\r\n                \"nearest_landmark\": null,\r\n                \"city\": null,\r\n                \"state\": \"Kaduna State\",\r\n                \"lga\": null,\r\n                \"gender\": \"Male\",\r\n                \"marital_status\": null,\r\n                \"rating\": null,\r\n                \"credit_score\": null,\r\n                \"risk_rating\": null,\r\n                \"selfie_bvn_check\": \"Successful\",\r\n                \"selfie_id_check\": null,\r\n                \"referred_by\": null,\r\n                \"referral_code\": \"EP4N9A\",\r\n                \"activated\": 1,\r\n                \"activated_on\": null,\r\n                \"last_login_date\": \"2024-08-10T23:07:48.000Z\",\r\n                \"blacklisted\": 0,\r\n                \"reason\": null,\r\n                \"created_on\": \"2024-08-10T23:07:48.000Z\"\r\n            }\r\n            \r\n        ]\r\n    },\r\n    \"meta\": {\r\n        \"cost\": 100,\r\n        \"balance\": 1555\r\n    }\r\n}"
								}
							]
						},
						{
							"name": "Update Customer",
							"request": {
								"method": "PATCH",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\r\n    \"first_name\": \"New Name\"\r\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}customers/:id",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										":id"
									],
									"variable": [
										{
											"key": "id",
											"value": ""
										}
									]
								},
								"description": "Update the information of an existing customer using their unique ID. Only the fields provided in the request body will be updated."
							},
							"response": [
								{
									"name": "Update Customer",
									"originalRequest": {
										"method": "PATCH",
										"header": [],
										"body": {
											"mode": "raw",
											"raw": "{\r\n    \"first_name\": \"New Name\"\r\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{base_url}}customers/:id",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												":id"
											],
											"variable": [
												{
													"key": "id",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": "{\r\n    \"status\": \"success\",\r\n    \"message\": \"Successful\",\r\n    \"data\": {\r\n        \"users\": [\r\n            {\r\n                \"id\": 00008999,\r\n                \"org_id\": 340015,\r\n                \"manager_id\": null,\r\n                \"office_id\": null,\r\n                \"first_name\": \"New Name\",\r\n                \"last_name\": \"User\",\r\n                \"phone_number\": \"23480123456789\",\r\n                \"country\": \"NGA\",\r\n                \"language\": \"en\",\r\n                \"locale\": \"en-US\",\r\n                \"timezone\": \"Africa/Lagos\",\r\n                \"email\": \"exampleuser@gmail.com\",\r\n                \"email_verified\": 0,\r\n                \"bvn\": \"22*******98\",\r\n                \"id_document_id\": null,\r\n                \"bvn_phone_number\": \"08169654518\",\r\n                \"bvn_validation_count\": 0,\r\n                \"dob\": \"1995-07-15T00:00:00.000Z\",\r\n                \"charged_for_id_verification\": 1,\r\n                \"photo_url\": \"https://documents.example.png\",\r\n                \"address\": null,\r\n                \"apartment_type\": null,\r\n                \"nearest_landmark\": null,\r\n                \"city\": null,\r\n                \"state\": \"Kaduna State\",\r\n                \"lga\": null,\r\n                \"gender\": \"Male\",\r\n                \"marital_status\": null,\r\n                \"rating\": null,\r\n                \"credit_score\": null,\r\n                \"risk_rating\": null,\r\n                \"selfie_bvn_check\": \"Successful\",\r\n                \"selfie_id_check\": null,\r\n                \"referred_by\": null,\r\n                \"referral_code\": \"EP4N9A\",\r\n                \"activated\": 1,\r\n                \"activated_on\": null,\r\n                \"last_login_date\": \"2024-08-10T23:07:48.000Z\",\r\n                \"blacklisted\": 0,\r\n                \"reason\": null,\r\n                \"created_on\": \"2024-08-10T23:07:48.000Z\"\r\n            }\r\n            \r\n        ]\r\n    },\r\n    \"meta\": {\r\n        \"cost\": 100,\r\n        \"balance\": 1555\r\n    }\r\n}"
								}
							]
						}
					],
					"description": "This section includes APIs related to customer management. It allows for creating, retrieving, updating, and deleting customer information, as well as managing customer profiles and documents. These APIs provide essential tools for handling customer data efficiently.",
					"event": [
						{
							"listen": "prerequest",
							"script": {
								"type": "text/javascript",
								"exec": [
									"\r",
									""
								]
							}
						},
						{
							"listen": "test",
							"script": {
								"type": "text/javascript",
								"packages": {},
								"exec": [
									""
								]
							}
						}
					]
				},
				{
					"name": "Accounts",
					"item": [
						{
							"name": "Get Customer Bank Accounts",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}customers/:id/bank-accounts",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										":id",
										"bank-accounts"
									],
									"variable": [
										{
											"key": "id",
											"value": ""
										}
									]
								},
								"description": "Retrieve a list of bank accounts associated with a specific customer by their unique ID. This endpoint is useful for displaying current bank account details on user profiles or for auditing purposes.\n\n**Response:** Returns an array of bank accounts, including details such as account number, bank code, and account name."
							},
							"response": [
								{
									"name": "Get Customer Bank Accounts",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}customers/:id/bank-accounts",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												":id",
												"bank-accounts"
											],
											"variable": [
												{
													"key": "id",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						},
						{
							"name": "Add Customer Bank Account",
							"request": {
								"method": "POST",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\r\n  \"account_number\": \"\",\r\n  \"bank_code\": \"068\",\r\n  \"account_name\": \"\",\r\n  \"account_type\": \"bank\"\r\n}\r\n",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}customers/:id/bank-accounts",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										":id",
										"bank-accounts"
									],
									"variable": [
										{
											"key": "id",
											"value": ""
										}
									]
								},
								"description": "Add a new bank account for a specific customer by their unique ID.\n\n- **Request:** Requires bank account details including account number, bank code, account name, and account type.\n    \n- **Response:** Confirms the addition of the bank account or returns an error if the operation fails."
							},
							"response": [
								{
									"name": "Add Customer Bank Account",
									"originalRequest": {
										"method": "POST",
										"header": [],
										"body": {
											"mode": "raw",
											"raw": "{\r\n  \"account_number\": \"\",\r\n  \"bank_code\": \"068\",\r\n  \"account_name\": \"\",\r\n  \"account_type\": \"bank\"\r\n}\r\n",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{base_url}}customers/:id/bank-accounts",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												":id",
												"bank-accounts"
											],
											"variable": [
												{
													"key": "id",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						},
						{
							"name": "Delete Customer Bank Account",
							"request": {
								"method": "DELETE",
								"header": [],
								"url": {
									"raw": "{{base_url}}customers/:id/bank-accounts/:bankAccountId",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										":id",
										"bank-accounts",
										":bankAccountId"
									],
									"variable": [
										{
											"key": "id",
											"value": ""
										},
										{
											"key": "bankAccountId",
											"value": ""
										}
									]
								},
								"description": "Delete a specific bank account associated with a customer by their unique ID and the bank account ID.\n\n**Response:** Confirms the deletion of the bank account or provides an error message if the deletion could not be processed."
							},
							"response": [
								{
									"name": "Delete Customer Bank Account",
									"originalRequest": {
										"method": "DELETE",
										"header": [],
										"url": {
											"raw": "{{base_url}}customers/:id/bank-accounts/:bankAccountId",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												":id",
												"bank-accounts",
												":bankAccountId"
											],
											"variable": [
												{
													"key": "id",
													"value": ""
												},
												{
													"key": "bankAccountId",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						}
					],
					"description": "APIs in this section manage customer bank accounts. They include endpoints for retrieving, adding, and deleting bank accounts associated with a customer. These APIs enable efficient management of customer bank account details, ensuring accurate and up-to-date information is maintained."
				},
				{
					"name": "Direct Debit",
					"item": [
						{
							"name": "Get Customer direct debits mandate",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}customers/:id/direct-debit-mandates",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										":id",
										"direct-debit-mandates"
									],
									"variable": [
										{
											"key": "id",
											"value": ""
										}
									]
								},
								"description": "Retrieve a list of direct debit mandates associated with a specific customer by their unique ID."
							},
							"response": [
								{
									"name": "Get Customer direct debits mandate",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}customers/:id/direct-debit-mandates",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												":id",
												"direct-debit-mandates"
											],
											"variable": [
												{
													"key": "id",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						},
						{
							"name": "Add Customer Direct Debit Mandate",
							"request": {
								"method": "POST",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\r\n  \"account_number\": \"12345\",\r\n  \"bank_code\": \"058\",\r\n  \"amount\": 120,\r\n  \"start_date\": \"2024-08-28T00:00:00.000Z\",\r\n  \"user_id\": 1000\r\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}customers/direct-debit-mandates",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										"direct-debit-mandates"
									]
								},
								"description": "Create a new direct debit mandate for a specific customer.\n\n- **Request:** Requires customer details, bank account information, and mandate specifics such as amount and frequency.\n    \n- **Response:** Returns the details of the newly created mandate, including its unique identifier and status."
							},
							"response": [
								{
									"name": "Add Customer Direct Debit Mandate",
									"originalRequest": {
										"method": "POST",
										"header": [],
										"body": {
											"mode": "raw",
											"raw": "{\r\n  \"account_number\": \"12345\",        // Required: Must be at least 5 characters\r\n  \"schedule\": true,                 // Optional: Defaults to true if not provided\r\n  \"bank_code\": \"123\",               // Required: Must be between 1 and 5 characters\r\n  \"email\": \"example@example.com\",   // Required: Must be a valid email format\r\n  \"phone_number\": \"01234567890\",    // Required: Must be exactly 11 characters\r\n  \"start_date\": \"2024-08-01\",       // Required: Must be in ISO date format\r\n  \"end_date\": \"2024-09-01\",         // Required: Must be in ISO date format\r\n  \"narration\": \"Sample narration\",  // Required\r\n  \"address\": \"123 Sample Street\",   // Required\r\n  \"mandate_file_url\": \"http://example.com/mandate.pdf\", // Optional\r\n  \"payment_start_date\": \"2024-08-10\", // Required: Must be in ISO date format\r\n  \"number_of_payments\": 5,          // Required: Must be at least 1\r\n  \"amount\": 100.0,                  // Required: Must be at least 1\r\n  \"minimum_amount\": 50.0,           // Optional\r\n  \"frequency\": \"monthly\",           // Optional: Replace with a valid value from config.direct_debit.debit_frequency\r\n  \"debit_type\": \"fixed\",            // Optional: Replace with a valid value from config.direct_debit.debit_type\r\n  \"activation_type\": \"manual\",      // Optional: Defaults to 'manual' if not provided\r\n  \"invite\": false                   // Optional: Defaults to false if not provided\r\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{base_url}}customers/direct-debit-mandates",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												"direct-debit-mandates"
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": "{\r\n    \"status\": \"success\",\r\n    \"message\": \"Mandate created successfully\",\r\n    \"data\": {\r\n        \"id\": 16391,\r\n        \"org_id\": 300000,\r\n        \"user_id\": 10000,\r\n        \"guarantor_id\": null,\r\n        \"amount\": 150,\r\n        \"activation_fee\": 0,\r\n        \"activation_charge_attempt\": 0,\r\n        \"last_activation_charge_attempt\": null,\r\n        \"activation_fee_transaction_id\": null,\r\n        \"mandate_type\": \"NIBSS-EASYPAY\",\r\n        \"activation_type\": \"emandate\",\r\n        \"max_no_of_debits\": \"\",\r\n        \"is_active\": 0,\r\n        \"status\": \"pending_mandate_activation\",\r\n        \"reference\": \"fed646d9-4b5f-4fee-b957-03ebb03935f4\",\r\n        \"start_date\": \"2024-08-28T00:00:00.000Z\",\r\n        \"end_date\": \"2026-08-28T00:00:00.000Z\",\r\n        \"registration_date\": \"2024-08-28T00:00:00.000Z\",\r\n        \"activation_date\": null,\r\n        \"meta_data\": null,\r\n        \"payer_name\": \"Example user\",\r\n        \"payer_email\": \"example@email.com\",\r\n        \"payer_phone\": \"2348123456789\",\r\n        \"payer_bank_code\": \"058\",\r\n        \"payer_account\": \"12345\",\r\n        \"bank_name\": \"\",\r\n        \"form_link_url\": null,\r\n        \"description\": \"Repayment of personal loan\",\r\n        \"request_id\": \"1724847405627\",\r\n        \"mandate_id\": \"RC00001/1007/000404907\",\r\n        \"meta\": null,\r\n        \"provider_status\": null,\r\n        \"channel\": null,\r\n        \"last_activity_date\": null,\r\n        \"created_on\": \"2024-08-28T12:16:45.000Z\",\r\n        \"created_by\": null,\r\n        \"modified_on\": \"2024-08-28T12:16:47.000Z\",\r\n        \"modified_by\": null,\r\n        \"deleted_flag\": 0,\r\n        \"deleted_on\": null\r\n    },\r\n    \"meta\": {\r\n        \"cost\": 100,\r\n        \"balance\": 1750\r\n    }\r\n}"
								}
							]
						},
						{
							"name": "Activate Customer Direct Debit Mandate",
							"request": {
								"method": "PATCH",
								"header": [],
								"url": {
									"raw": "{{base_url}}customers/direct-debit-mandates/:mandateId/activate",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										"direct-debit-mandates",
										":mandateId",
										"activate"
									],
									"variable": [
										{
											"key": "mandateId",
											"value": ""
										}
									]
								},
								"description": "Activate a specific direct debit mandate for a customer by the mandate ID."
							},
							"response": [
								{
									"name": "Activate Customer Direct Debit Mandate",
									"originalRequest": {
										"method": "PATCH",
										"header": [],
										"url": {
											"raw": "{{base_url}}customers/direct-debit-mandates/:mandateId/activate",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												"direct-debit-mandates",
												":mandateId",
												"activate"
											],
											"variable": [
												{
													"key": "mandateId",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						},
						{
							"name": "Deactivate Customer Direct Debit Mandate",
							"request": {
								"method": "PATCH",
								"header": [],
								"url": {
									"raw": "{{base_url}}customers/direct-debit-mandates/:mandateId/deactivate",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										"direct-debit-mandates",
										":mandateId",
										"deactivate"
									],
									"variable": [
										{
											"key": "mandateId",
											"value": ""
										}
									]
								},
								"description": "Deactivate a specific direct debit mandate for a customer by the mandate ID"
							},
							"response": [
								{
									"name": "Deactivate Customer Direct Debit Mandate",
									"originalRequest": {
										"method": "PATCH",
										"header": [],
										"url": {
											"raw": "{{base_url}}customers/direct-debit-mandates/:mandateId/deactivate",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												"direct-debit-mandates",
												":mandateId",
												"deactivate"
											],
											"variable": [
												{
													"key": "mandateId",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						},
						{
							"name": "Cancel Customer Direct Debit Mandate",
							"request": {
								"method": "PATCH",
								"header": [],
								"url": {
									"raw": "{{base_url}}customers/direct-debit-mandates/:mandateId/cancel",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										"direct-debit-mandates",
										":mandateId",
										"cancel"
									],
									"variable": [
										{
											"key": "mandateId",
											"value": ""
										}
									]
								},
								"description": "Cancel a specific direct debit mandate for a customer by their unique ID and the mandate ID."
							},
							"response": [
								{
									"name": "Cancel Customer Direct Debit Mandate",
									"originalRequest": {
										"method": "PATCH",
										"header": [],
										"url": {
											"raw": "{{base_url}}customers/direct-debit-mandates/:mandateId/cancel",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												"direct-debit-mandates",
												":mandateId",
												"cancel"
											],
											"variable": [
												{
													"key": "mandateId",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						}
					],
					"description": "This section provides APIs for managing direct debit mandates. It includes endpoints to create, activate, deactivate, and cancel direct debit mandates for customers."
				},
				{
					"name": "Loans",
					"item": [
						{
							"name": "Get Loan Products",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}loan-products",
									"host": [
										"{{base_url}}loan-products"
									],
									"query": [
										{
											"key": "limit",
											"value": "",
											"disabled": true
										},
										{
											"key": "max_amount",
											"value": "",
											"disabled": true
										},
										{
											"key": "interest",
											"value": "",
											"disabled": true
										},
										{
											"key": "status",
											"value": "",
											"disabled": true
										}
									]
								},
								"description": "Retrieve a list of available loan products."
							},
							"response": [
								{
									"name": "Get Loan Products",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}loan-products",
											"host": [
												"{{base_url}}loan-products"
											],
											"query": [
												{
													"key": "limit",
													"value": "",
													"disabled": true
												},
												{
													"key": "max_amount",
													"value": "",
													"disabled": true
												},
												{
													"key": "interest",
													"value": "",
													"disabled": true
												},
												{
													"key": "status",
													"value": "",
													"disabled": true
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						},
						{
							"name": "Score Loan",
							"request": {
								"method": "POST",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\r\n  \"product_id\": 2 ,\r\n  \"bvn\": \"\",\r\n  \"requested_amount\": 100,\r\n  \"location\": \"Lagos\"\r\n}\r\n",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}customers/loans/score",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										"loans",
										"score"
									]
								},
								"description": "Get the eligibility of a customer for a loan by scoring them against the loan product's scoring model."
							},
							"response": [
								{
									"name": "Score Loan",
									"originalRequest": {
										"method": "POST",
										"header": [],
										"body": {
											"mode": "raw",
											"raw": "{\r\n  \"product_id\": 2 ,\r\n  \"bvn\": \"\",\r\n  \"requested_amount\": 100,\r\n  \"location\": \"Lagos\"\r\n}\r\n",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{base_url}}customers/loans/score",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												"loans",
												"score"
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						},
						{
							"name": "Get Customer Loan",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}customers/loans/:loanId",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										"loans",
										":loanId"
									],
									"variable": [
										{
											"key": "loanId",
											"value": ""
										}
									]
								},
								"description": "Retrieves details of a loan taken by a customer. It requires both the loan's unique ID."
							},
							"response": [
								{
									"name": "Get Customer Loan",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}customers/loans/:loanId",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												"loans",
												":loanId"
											],
											"variable": [
												{
													"key": "loanId",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						},
						{
							"name": "Get Customer Loans",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}customers/:id/loans",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										":id",
										"loans"
									],
									"variable": [
										{
											"key": "id",
											"value": ""
										}
									]
								},
								"description": "Retrieves the list of all loans taken by a specific customer based on their unique ID."
							},
							"response": [
								{
									"name": "Get Customer Loans",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}customers/:id/loans",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												":id",
												"loans"
											],
											"variable": [
												{
													"key": "id",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						},
						{
							"name": "Book Loan",
							"request": {
								"method": "POST",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\r\n  \"bvn\": \"\",                      // Required\r\n  \"requested_amount\": 300,                 // Required\r\n  \"proposed_tenor\": 12,                      // Required\r\n  \"proposed_tenor_period\": \"months\",         // Optional, accepts: \"days\", \"weeks\", \"months\", \"Months\", \"Days\", \"Weeks\"\r\n  \"purpose\": \"Home renovation\",              // Optional, can be null\r\n  \"marital_status\": \"Single\",                // Optional, can be null\r\n  \"no_of_dependent\": \"2\",                    // Optional, can be null\r\n  \"type_of_residence\": \"Rented\",             // Optional, can be null\r\n  \"educational_attainment\": \"Bachelor's\",    // Optional, can be null\r\n  \"sector_of_employment\": \"Technology\",      // Optional, can be null\r\n  \"monthly_net_income\": \"100000\",            // Optional, can be null\r\n  \"proposed_payday\": \"2024-08-30\",           // Optional\r\n  \"employment_status\": \"Full-time\",          // Optional, can be null\r\n  \"work_start_date\": \"2022-01-15\",           // Optional, can be null\r\n  \"work_email\": \"user@company.com\",          // Optional, can be null or an empty string\r\n  \"current_employer\": \"Company Inc.\",        // Optional\r\n  \"employment_category\": \"Permanent\",        // Optional\r\n  \"product_id\": 74,                       // Required\r\n  \"disburse_to\": \"bank\",                     // Optional, defaults to \"bank\"\r\n  \"location\": \"Lagos\"                        // Optional, can be null or an empty string\r\n}\r\n",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}customers/loans",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										"loans"
									]
								},
								"description": "Book a loan using the details of the customer."
							},
							"response": [
								{
									"name": "Book Loan",
									"originalRequest": {
										"method": "POST",
										"header": [],
										"body": {
											"mode": "raw",
											"raw": "{\r\n  \"bvn\": \"\",                      // Required\r\n  \"requested_amount\": 300,                 // Required\r\n  \"proposed_tenor\": 12,                      // Required\r\n  \"proposed_tenor_period\": \"months\",         // Optional, accepts: \"days\", \"weeks\", \"months\", \"Months\", \"Days\", \"Weeks\"\r\n  \"purpose\": \"Home renovation\",              // Optional, can be null\r\n  \"marital_status\": \"Single\",                // Optional, can be null\r\n  \"no_of_dependent\": \"2\",                    // Optional, can be null\r\n  \"type_of_residence\": \"Rented\",             // Optional, can be null\r\n  \"educational_attainment\": \"Bachelor's\",    // Optional, can be null\r\n  \"sector_of_employment\": \"Technology\",      // Optional, can be null\r\n  \"monthly_net_income\": \"100000\",            // Optional, can be null\r\n  \"proposed_payday\": \"2024-08-30\",           // Optional\r\n  \"employment_status\": \"Full-time\",          // Optional, can be null\r\n  \"work_start_date\": \"2022-01-15\",           // Optional, can be null\r\n  \"work_email\": \"user@company.com\",          // Optional, can be null or an empty string\r\n  \"current_employer\": \"Company Inc.\",        // Optional\r\n  \"employment_category\": \"Permanent\",        // Optional\r\n  \"product_id\": 74,                       // Required\r\n  \"disburse_to\": \"bank\",                     // Optional, defaults to \"bank\"\r\n  \"location\": \"Lagos\"                        // Optional, can be null or an empty string\r\n}\r\n",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{base_url}}customers/loans",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												"loans"
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						},
						{
							"name": "Approve Loan",
							"request": {
								"method": "PUT",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\r\n  \"beneficiary_id\": null,                      // Optional, can be null or an empty string\r\n  \"account_number\": \"\",                        // Optional, can be null or an empty string, default is \"\"\r\n  \"bank_code\": \"\",                             // Optional, can be null or an empty string, default is \"\"\r\n  \"disbursement_provider\": \"\",                 // Optional, can be null or an empty string, default is \"\"\r\n  \"account_name\": \"\",                          // Optional, can be null or an empty string, default is \"\"\r\n  \"beneficiary_email\": \"\",                     // Optional, can be null or an empty string, default is \"\"\r\n  \"beneficiary_phone_number\": \"\",              // Optional, can be null or an empty string, default is \"\"\r\n  \"bank_name\": \"\",                             // Optional, can be null or an empty string, default is \"\"\r\n  \"attributes\": {                              // Optional, loan attributes\r\n    \"key1\": \"value1\",\r\n    \"key2\": \"value2\"\r\n  }\r\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}customers/loans/:loanId/",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										"loans",
										":loanId",
										""
									],
									"variable": [
										{
											"key": "loanId",
											"value": ""
										}
									]
								},
								"description": "Approve a loan booked for a customer using the loan's unique ID."
							},
							"response": [
								{
									"name": "Approve Loan",
									"originalRequest": {
										"method": "PUT",
										"header": [],
										"body": {
											"mode": "raw",
											"raw": "{\r\n  \"beneficiary_id\": null,                      // Optional, can be null or an empty string\r\n  \"account_number\": \"\",                        // Optional, can be null or an empty string, default is \"\"\r\n  \"bank_code\": \"\",                             // Optional, can be null or an empty string, default is \"\"\r\n  \"disbursement_provider\": \"\",                 // Optional, can be null or an empty string, default is \"\"\r\n  \"account_name\": \"\",                          // Optional, can be null or an empty string, default is \"\"\r\n  \"beneficiary_email\": \"\",                     // Optional, can be null or an empty string, default is \"\"\r\n  \"beneficiary_phone_number\": \"\",              // Optional, can be null or an empty string, default is \"\"\r\n  \"bank_name\": \"\",                             // Optional, can be null or an empty string, default is \"\"\r\n  \"attributes\": {                              // Optional, loan attributes\r\n    \"key1\": \"value1\",\r\n    \"key2\": \"value2\"\r\n  }\r\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{base_url}}customers/loans/:loanId/",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												"loans",
												":loanId",
												""
											],
											"variable": [
												{
													"key": "loanId",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						},
						{
							"name": "Repay Customer Loan",
							"request": {
								"method": "POST",
								"header": [],
								"body": {
									"mode": "raw",
									"raw": "{\r\n  \"amount\": 100000.50,\r\n  \"comment\": \"Payment for invoice #12345\",\r\n  \"reference\": null,\r\n  \"channel\": \"bank_transfer\"\r\n}",
									"options": {
										"raw": {
											"language": "json"
										}
									}
								},
								"url": {
									"raw": "{{base_url}}customers/loans/:loanId/repay",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										"loans",
										":loanId",
										"repay"
									],
									"variable": [
										{
											"key": "loanId",
											"value": ""
										}
									]
								},
								"description": "Repay a specific loan for a customer by the loan ID."
							},
							"response": [
								{
									"name": "Repay Customer Loan",
									"originalRequest": {
										"method": "POST",
										"header": [],
										"body": {
											"mode": "raw",
											"raw": "{\r\n  \"amount\": 100000.50,\r\n  \"comment\": \"Payment for invoice #12345\",\r\n  \"reference\": null,\r\n  \"channel\": \"bank_transfer\"\r\n}",
											"options": {
												"raw": {
													"language": "json"
												}
											}
										},
										"url": {
											"raw": "{{base_url}}customers/loans/:loanId/repay",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												"loans",
												":loanId",
												"repay"
											],
											"variable": [
												{
													"key": "loanId",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						}
					],
					"description": "This section contains APIs related to loan management. It includes endpoints for retrieving loan products, scoring loan applications, getting loan schedules, booking loans, retrieving customer loans, and repaying loans."
				},
				{
					"name": "Cards",
					"item": [
						{
							"name": "Get Customer cards",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}customers/:id/cards",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										":id",
										"cards"
									],
									"variable": [
										{
											"key": "id",
											"value": ""
										}
									]
								},
								"description": "Retrieve a list of cards associated with a specific customer by their unique ID."
							},
							"response": [
								{
									"name": "Get Customer cards",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}customers/:id/cards",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												":id",
												"cards"
											],
											"variable": [
												{
													"key": "id",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						},
						{
							"name": "Deactivate Customer Card",
							"request": {
								"method": "PATCH",
								"header": [],
								"url": {
									"raw": "{{base_url}}customers/:id/cards/:cardId",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										":id",
										"cards",
										":cardId"
									],
									"variable": [
										{
											"key": "id",
											"value": ""
										},
										{
											"key": "cardId",
											"value": ""
										}
									]
								},
								"description": "Deactivate a specific card associated with a customer by their unique ID and the card ID."
							},
							"response": [
								{
									"name": "Deactivate Customer Card",
									"originalRequest": {
										"method": "PATCH",
										"header": [],
										"url": {
											"raw": "{{base_url}}customers/:id/cards/:cardId",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												":id",
												"cards",
												":cardId"
											],
											"variable": [
												{
													"key": "id",
													"value": ""
												},
												{
													"key": "cardId",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						},
						{
							"name": "Delete Customer Card",
							"request": {
								"method": "DELETE",
								"header": [],
								"url": {
									"raw": "{{base_url}}customers/:id/cards/:cardId",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										":id",
										"cards",
										":cardId"
									],
									"variable": [
										{
											"key": "id",
											"value": ""
										},
										{
											"key": "cardId",
											"value": ""
										}
									]
								},
								"description": "Delete a specific card associated with a customer by their unique ID and the card ID."
							},
							"response": [
								{
									"name": "Delete Customer Card",
									"originalRequest": {
										"method": "DELETE",
										"header": [],
										"url": {
											"raw": "{{base_url}}customers/:id/cards/:cardId",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												":id",
												"cards",
												":cardId"
											],
											"variable": [
												{
													"key": "id",
													"value": ""
												},
												{
													"key": "cardId",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						}
					],
					"description": "APIs in this section manage customer cards. It includes endpoints for retrieving, deactivating, and deleting cards associated with a customer."
				},
				{
					"name": "Wallet",
					"item": [
						{
							"name": "Get Customer wallets",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}customers/:id/wallets",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										":id",
										"wallets"
									],
									"variable": [
										{
											"key": "id",
											"value": ""
										}
									]
								},
								"description": "Retrieve a list of wallets created for a customer by their unique ID."
							},
							"response": [
								{
									"name": "Get Customer wallets",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}customers/:id/wallets",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												":id",
												"wallets"
											],
											"variable": [
												{
													"key": "id",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						},
						{
							"name": "Get Customer wallet transaction",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}customers/:id/wallets/:walletId/transactions",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										":id",
										"wallets",
										":walletId",
										"transactions"
									],
									"variable": [
										{
											"key": "id",
											"value": ""
										},
										{
											"key": "walletId",
											"value": ""
										}
									]
								},
								"description": "Retrieve a list of transactions for a specific wallet by the customer's unique ID and the wallet ID."
							},
							"response": [
								{
									"name": "Get Customer wallet transaction",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}customers/:id/wallets/:walletId/transactions",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												":id",
												"wallets",
												":walletId",
												"transactions"
											],
											"variable": [
												{
													"key": "id",
													"value": ""
												},
												{
													"key": "walletId",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						},
						{
							"name": "Transfer to Customer Wallet",
							"request": {
								"method": "POST",
								"header": [],
								"url": {
									"raw": "{{base_url}}customers/:id/wallets/:walletId/transactions",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										":id",
										"wallets",
										":walletId",
										"transactions"
									],
									"variable": [
										{
											"key": "id",
											"value": ""
										},
										{
											"key": "walletId",
											"value": ""
										}
									]
								},
								"description": "Transfer funds to a specific wallet by the customer's unique ID and the wallet ID."
							},
							"response": [
								{
									"name": "Transfer to Customer Wallet",
									"originalRequest": {
										"method": "POST",
										"header": [],
										"url": {
											"raw": "{{base_url}}customers/:id/wallets/:walletId/transactions",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												":id",
												"wallets",
												":walletId",
												"transactions"
											],
											"variable": [
												{
													"key": "id",
													"value": ""
												},
												{
													"key": "walletId",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						}
					],
					"description": "This section provides APIs for managing customer wallets. It includes endpoints for retrieving wallets, retrieving wallet transactions, and transferring funds to customer wallets. These APIs enable comprehensive management of virtual wallets and transactions."
				},
				{
					"name": "Logs",
					"item": [
						{
							"name": "Get Customer Logs",
							"request": {
								"method": "GET",
								"header": [],
								"url": {
									"raw": "{{base_url}}customers/:id/logs",
									"host": [
										"{{base_url}}customers"
									],
									"path": [
										":id",
										"logs"
									],
									"variable": [
										{
											"key": "id",
											"value": ""
										}
									]
								},
								"description": "Retrieve logs related to a specific customer's activities by their unique ID."
							},
							"response": [
								{
									"name": "Get Customer Logs",
									"originalRequest": {
										"method": "GET",
										"header": [],
										"url": {
											"raw": "{{base_url}}customers/:id/logs",
											"host": [
												"{{base_url}}customers"
											],
											"path": [
												":id",
												"logs"
											],
											"variable": [
												{
													"key": "id",
													"value": ""
												}
											]
										}
									},
									"_postman_previewlanguage": "Text",
									"header": null,
									"cookie": [],
									"body": null
								}
							]
						}
					],
					"description": "APIs in this section are used to retrieve logs related to customer activities. It helps in monitoring and auditing customer interactions with the platform, providing insights into user behavior and system performance."
				}
			],
			"description": "This section details the APIs that facilitate core operations for managing customers, accounts, direct debits, cards, loans, transactions, and logs. These APIs are integral to developing custom loan applications and seamlessly integrating with Lendsqr's platform.\n\n### Authentication and Token Management\n\n#### Accessing Core Services APIs\n\nTo interact with any API within this core services collection (excluding the `Auth` endpoint), the following authentication mechanisms must be implemented:\n\n- **Bearer Token:** This token, which serves as the API key, is generated via your application on Adjutor.\n    \n- **x-access-token Header:** This token is retrieved from the Auth endpoint. After providing valid credentials (email and password) in the request body, the response will include the token. This token must be included in the headers of subsequent API requests as `x-access-token`.\n    \n\n#### Steps to Obtain Authentication Tokens\n\n1. **Lendsqr Admin Console Sign-Up:**\n    \n    - Create an account on the [Lendsqr admin console](https://app.lendsqr.com) to initiate the process.\n        \n2. **Team Member Setup:**\n    \n    - Add a team member to your organization using a unique email. This member will manage all API interactions through the admin console. [Learn more](https://lendsqr.freshdesk.com/support/solutions/articles/44002359125-how-to-add-a-team-member)\n        \n3. **Adjutor Access and API Key Generation:**\n    \n    - The designated team member can access the [Adjutor](https://app.adjutor.io) platform with the credentials set up on the admin console. Once logged in, they can create an application and retrieve the API key, which acts as the Bearer Token.\n        \n4. **Auth Endpoint Token Retrieval:**\n    \n    - Use the email and password of the team member to call the Auth endpoint. The response will include the `x-access-token`, which must be included in the header of all core service API requests.\n        \n\n#### Important Considerations\n\n- Once the team member's credentials have been used to authenticate API calls, those credentials will no longer be valid for accessing the admin console. Ensure proper management of credentials to maintain access control.",
			"event": [
				{
					"listen": "prerequest",
					"script": {
						"exec": [
							"const baseURL = pm.environment.get(\"base_url\");\r",
							"const apiKey = pm.environment.get(\"bearerToken\");\r",
							"const email = pm.environment.get(\"email\");\r",
							"const password = pm.environment.get(\"password\");\r",
							"\r",
							"pm.sendRequest({\r",
							"    url: `${baseURL}/customers/auth`,\r",
							"    method: 'POST',\r",
							"    header: {\r",
							"        'Content-Type': 'application/json',\r",
							"        'Authorization': `Bearer ${apiKey}`\r",
							"    },\r",
							"    body: {\r",
							"        mode: 'raw',\r",
							"        raw: JSON.stringify({\r",
							"            email: email,\r",
							"            password: password\r",
							"        })\r",
							"    }\r",
							"}, function (err, res) {\r",
							"    if (err) {\r",
							"        console.log(err);\r",
							"        return;\r",
							"    }\r",
							"    const response = res.json();\r",
							"    const token = response.token;\r",
							"\r",
							"    if (token) {\r",
							"        pm.environment.set(\"x-access-token\", token);  // Save token to environment\r",
							"        pm.request.headers.upsert({ key: 'x-access-token', value: token });  // Update request header\r",
							"    } else {\r",
							"        console.log('Token not found in response.');\r",
							"    }\r",
							"});\r",
							""
						],
						"type": "text/javascript"
					}
				}
			]
		}
	],
	"auth": {
		"type": "bearer",
		"bearer": [
			{
				"key": "token",
				"value": "{{access_token}}",
				"type": "string"
			}
		]
	},
	"event": [
		{
			"listen": "prerequest",
			"script": {
				"type": "text/javascript",
				"exec": [
					""
				]
			}
		},
		{
			"listen": "test",
			"script": {
				"type": "text/javascript",
				"exec": [
					""
				]
			}
		}
	],
	"variable": [
		{
			"key": "base_url",
			"value": "https://adjutor.lendsqr.com/v2/",
			"type": "string"
		},
		{
			"key": "access_token",
			"value": "sk_live_Hfvcf9srOs5pPWDporlAOWpDqrjon0y9PeUysTtB",
			"type": "string"
		},
		{
			"key": "access_token",
			"value": "",
			"type": "string",
			"disabled": true
		},
		{
			"key": "x_access_token",
			"value": "",
			"type": "string"
		}
	]
}ding Adjutor API Service.postman_collection.json…]()
