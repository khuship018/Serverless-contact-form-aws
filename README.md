**Serverless Contact Form — AWS**
- A zero-server contact form that saves submissions to DynamoDB and emails you instantly via SES. Built with plain HTML and powered entirely by AWS serverless services — no EC2, no maintenance, no cost when idle.

**Architecture**
S3 → API Gateway → Lambda → DynamoDB + SES

**Steps**
**DynamoDB Table**

Step 1: Open the AWS Console and navigate to DynamoDB.
<img width="1914" height="871" alt="image" src="https://github.com/user-attachments/assets/635e8681-7685-4871-be8d-bd3fa6fd6f19" />

Step 2: In DynamoDB, go to **Tables** and click on **Create Table**.
<img width="1920" height="911" alt="image" src="https://github.com/user-attachments/assets/27df54a1-7ff6-4caf-ad16-131677f377d5" />

Step 3: Enter a table name, set the partition key to **“id”** (String), keep the default settings, and click **Create Table**.
<img width="1916" height="880" alt="image" src="https://github.com/user-attachments/assets/094b3f20-d7b8-4bf7-ae30-d3b1a4874ea8" />
<img width="1920" height="834" alt="image" src="https://github.com/user-attachments/assets/dee2e7c0-31b3-4a01-a037-2f59b7b00c72" />

**Lamda function**

Before creating the Lambda function, you need to install a few dependencies. Follow these steps:

1. Create a project folder:

```
mkdir contact-form-lambda
cd contact-form-lambda
```

2. Open the folder in your preferred code editor (preferably VS Code), then open the terminal and initialize a Node.js project:

```
npm init -y
```

3. Install the required AWS SDK packages:

```
npm install @aws-sdk/client-dynamodb @aws-sdk/lib-dynamodb
```


Now continue with the steps in the AWS Console:

Step 1: Search for **Lambda** in the AWS Console and open it.
<img width="1912" height="836" alt="image" src="https://github.com/user-attachments/assets/cb274e57-8e30-45b9-a873-431f13b2aaae" />

Step 2: In Lambda, go to **Functions** and click on **Create function**.
<img width="1920" height="924" alt="image" src="https://github.com/user-attachments/assets/7bc2c706-be94-40d2-b1d5-94a59205ffd4" />

Step 3: Enter a name for the function, keep the default settings unchanged, and proceed.
<img width="1920" height="870" alt="image" src="https://github.com/user-attachments/assets/f609f4eb-b7f7-449d-909e-f8555e1e7c6c" />

Step 4: In the code section, click on **Upload from** and select **.zip file**.
<img width="1920" height="910" alt="image" src="https://github.com/user-attachments/assets/650f148e-fdf3-4dde-bc59-0407c5d3724a" />

Step 5: Select your `.zip` file and upload it.

**Note:** Do not zip the main folder itself. Instead, open the folder (where `node_modules`, `index.js`, etc. are present), select all the files inside it, and then create the zip.

The `index.html` and other required files are available in the repository—please refer to them.
<img width="1024" height="385" alt="image" src="https://github.com/user-attachments/assets/2b6079f9-e36b-4733-8c6e-74e5406846f3" />

Step 6: Go to **Configuration**, then **Permissions**, and click on the **Execution role**.
<img width="1918" height="908" alt="image" src="https://github.com/user-attachments/assets/60712b64-f909-42fc-8c2d-c948d54860b0" />

Step 7: After opening it, click on **Add permissions** and select **Attach policies**.
<img width="1920" height="870" alt="image" src="https://github.com/user-attachments/assets/18ef96db-c1cf-4d53-a16e-45c0bb75ab7a" />

Step 8: Search for **AmazonDynamoDBFullAccess** and **AmazonSESFullAccess**, select both policies, and click **Add permissions**.
<img width="1901" height="844" alt="image" src="https://github.com/user-attachments/assets/b8685b6e-5d3e-494f-aaae-b189a9864d26" />
<img width="1916" height="712" alt="image" src="https://github.com/user-attachments/assets/940c8edf-de54-4311-b325-2e3994799f76" />

Step 9: Go back to the **Code** section and create a sample test event.
<img width="1920" height="924" alt="image" src="https://github.com/user-attachments/assets/f4008568-d83d-48c8-8f4e-04b340606c01" />

Step 10: First, click **Deploy** to deploy your code, then run the test event. You should see the status as **Success**.
<img width="1904" height="898" alt="image" src="https://github.com/user-attachments/assets/afaf11dd-7c83-4cbb-adb3-bc18b564857d" />

**API Gateway**
Step 1: Search for **API Gateway** in the AWS Console and open it.
<img width="1916" height="908" alt="image" src="https://github.com/user-attachments/assets/ea93d7a6-5771-42a3-87dd-6546f610c9ba" />

Step 2: In API Gateway, go to **APIs** and click on **Create API**.
<img width="1905" height="843" alt="image" src="https://github.com/user-attachments/assets/d7c0647d-9195-4f97-a209-a8c3428994ec" />

Step 3: Select **HTTP API** and click on **Build**.
<img width="1920" height="847" alt="image" src="https://github.com/user-attachments/assets/f0ad24bb-223d-4615-a961-653e23439ea2" />

Step 4: Enter a name for the API, then add an integration. Choose **Lambda**, select your region and the Lambda function you created, and click **Save**.
<img width="1920" height="883" alt="image" src="https://github.com/user-attachments/assets/ca8c5f10-0f31-4378-92ab-edfe0f4c50e4" />

Step 5: Next, configure the routes. Select the **POST** method, set the resource path as required, and choose your Lambda function as the integration target.
<img width="1920" height="803" alt="image" src="https://github.com/user-attachments/assets/cd155f4e-4c6e-4632-a22d-ef954e57d6ee" />

Step 6: No changes are needed in **Stages**—leave the default settings as they are.
<img width="1920" height="849" alt="image" src="https://github.com/user-attachments/assets/8cd817af-b4ee-400b-92ac-e37b1b46896b" />

Step 7: Review and create
<img width="1911" height="869" alt="image" src="https://github.com/user-attachments/assets/e1bcca7f-16d1-4560-9ec7-81cb45f1dd3f" />

Step 8: After creating the API, open it and go to the **CORS** section. Add the following settings:

* **Access-Control-Allow-Origin:** *
* **Access-Control-Allow-Headers:** content-type
* **Access-Control-Allow-Methods:** POST
  
<img width="1920" height="898" alt="image" src="https://github.com/user-attachments/assets/e1ad4349-f0b9-4ef3-9e41-a3817ebfcea8" />


**SES(Simple Email Service)**

Step 1: Search for **Amazon SES** in the AWS Console and open it.
<img width="1916" height="918" alt="image" src="https://github.com/user-attachments/assets/c7fce21a-4a2a-408f-873d-d0110363ff12" />

Step 2: In Amazon SES, go to **Identities** and click on **Create identity**.
<img width="1919" height="908" alt="image" src="https://github.com/user-attachments/assets/88fea25b-7681-4512-ad25-df1caf292014" />

Step 3: Select **Email address**, then enter the email where you want to receive the form data.
<img width="1920" height="858" alt="image" src="https://github.com/user-attachments/assets/e0a74d65-b7a0-4dc6-90e0-fccc7343e081" />

Step 4: You’ll receive a verification email at the address you provided. Open it, click the verification link, and then return to the console.
<img width="1911" height="873" alt="image" src="https://github.com/user-attachments/assets/d474f707-66cf-452d-b9be-6f490289410b" />
<img width="1919" height="893" alt="image" src="https://github.com/user-attachments/assets/c0912c13-a919-4123-8da6-2de92443c9e0" />


**S3**

Step 1: Create a basic form file named **index.html** in your code editor (preferably VS Code).
This file is already provided in the repository—feel free to use it directly.

Step 2: Search for **Amazon S3** in the AWS Console and open it.
<img width="1919" height="915" alt="image" src="https://github.com/user-attachments/assets/fa223027-02a2-4253-a67d-2cd63f705a7d" />

Step 3: Create a new bucket, enter a name, uncheck **Block all public access**, select the acknowledgment checkbox, and then create the bucket.
<img width="1918" height="915" alt="image" src="https://github.com/user-attachments/assets/57395860-d67c-4af7-b6b7-3cf31d267e19" />
<img width="1897" height="675" alt="image" src="https://github.com/user-attachments/assets/61ae33eb-fc11-43bc-9881-28941f356d2b" />

Step 4: Open the bucket and upload the **index.html** file.
<img width="1920" height="849" alt="image" src="https://github.com/user-attachments/assets/34d5e2ea-401a-447e-bee9-77f8b468d93b" />

Step 5: Go to the **Permissions** tab of the bucket and add the bucket policy.
The required policy is already provided in the repository—copy and paste it from there.
<img width="1529" height="651" alt="image" src="https://github.com/user-attachments/assets/8c55ec5e-8fbc-41b7-ad63-2db712199633" />

Step 6: Step 6: Go to the **Properties** tab and enable **Static website hosting**.
<img width="1900" height="922" alt="image" src="https://github.com/user-attachments/assets/59abca47-aba6-4155-83de-e136580a4631" />


**Error you might face and things to look for**
You can check the error as right clicking and going to inspect inside console.
🔴 403 Forbidden
Add OPTIONS in CORS
Click Deploy after changes
Check API URL (path + stage must match)
🟠 400 Bad Request
Field names must match (name vs firstName)
Parse body → JSON.parse(event.body)
Otherwise validation will fail
🔥 500 Error (SES)
Verify sender email in SES
Replace dummy email (yourname@gmail.com)
Make sure SES status = Verified
💥 500 Error (General)
Use Node.js 18.x or 20.x
File name & handler must match
Use require OR set "type": "module"
DynamoDB table name must match exactly
IAM role needs PutItem permission
Region must be correct
