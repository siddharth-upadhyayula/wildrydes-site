AWS Integration in WildRydes Application

The application incorporates AWS services for backend logic, user authentication, data storage, and possibly other features like mapping and analytics. Here’s how AWS fits into the application:


<img width="1331" alt="Screenshot 2025-01-08 at 12 35 56 PM" src="https://github.com/user-attachments/assets/eb5922cf-6f83-41f8-a091-29f9e1aeb346" />


1. AWS Lambda
	•	Files: aws/lambda.js, aws/lambdaTest.js
	•	Purpose: Implements serverless backend logic. The Lambda functions likely handle:
	•	Backend operations such as storing ride requests or processing user data.
	•	Communication with other AWS services like Amazon DynamoDB or Amazon S3.
	•	Event-driven tasks triggered by frontend user actions (e.g., submitting a ride request).
	•	Testing: The lambdaTest.js file might include test cases or example events to simulate function executions locally or via the AWS Lambda console.

2. AWS Cognito
	•	File: js/cognito-auth.js
	•	Purpose: Manages user authentication and authorization.
	•	User registration, login, and token-based authentication workflows.
	•	User pool configuration to secure the application.
	•	Integration with AWS IAM roles for controlled access to other AWS resources.

3. AWS S3
	•	Purpose: Hosts static files (HTML, CSS, JS, images) for the web application.
	•	The images/ directory might contain assets uploaded to an S3 bucket.
	•	S3 could also be used for storing user-uploaded data (e.g., ride-related files).

4. Amazon DynamoDB
	•	Purpose: Likely used for database storage, such as:
	•	Ride details (pickup/drop-off locations, timestamps).
	•	User profiles and preferences.
	•	Session tracking or application logs.

5. Amazon API Gateway
	•	Purpose: Acts as a REST API interface between the frontend and AWS Lambda functions.
	•	Routes HTTP requests (e.g., booking a ride or verifying user accounts) to the appropriate backend function.
	•	Enables secure communication between the frontend and backend.

6. Amazon CloudFront
	•	Purpose: CDN for faster content delivery, ensuring the web application is accessible globally with reduced latency.

7. Mapbox Integration
	•	Though Mapbox is not an AWS service, it complements AWS by providing geolocation services, mapping, and ride tracking. These are likely tied to Lambda functions for real-time data handling.

Documentation for Repository

Repository Name: siddharth-upadhyayula-wildrydes-site

Description:

A web application that allows users to register, sign in, and book magical unicorn rides. This application leverages AWS services for serverless backend logic, user authentication, and data management, ensuring scalability and robust functionality.

Directory Structure

siddharth-upadhyayula-wildrydes-site/
├── README.md
├── HTML Files: Core web pages (apply, FAQ, register, etc.)
├── aws/: Contains Lambda function code.
├── css/: Stylesheets for the UI.
├── fonts/: Font resources.
├── images/: Image assets.
├── js/: Core scripts, including AWS Cognito integration and mapping features.

Prerequisites
	1.	AWS Account: Ensure you have an AWS account with access to:
	•	Lambda
	•	API Gateway
	•	Cognito
	•	DynamoDB
	•	S3
	•	CloudFront
	2.	Node.js: Install for local testing of Lambda functions.
	3.	Mapbox Account: Required for mapping functionality.

Setup Instructions
	1.	Clone the Repository:
 
```
git clone https://github.com/siddharth-upadhyayula/wildrydes-site.git
cd siddharth-upadhyayula-wildrydes-site
```

	2.	Frontend Setup:
	•	Update config.js with your AWS Cognito pool ID, API Gateway URL, and Mapbox token.
	•	Host HTML and CSS files on S3 or a local development server.
	3.	AWS Lambda Deployment:
	•	Zip lambda.js and its dependencies.
	•	Deploy the zip file via the AWS Lambda console or CLI:
 
```
aws lambda create-function \
    --function-name WildRydesLambda \
    --runtime nodejs20.x \
    --role <IAM-ROLE-ARN> \
    --handler lambda.handler \
    --zip-file fileb://lambda.zip
```

	4.	API Gateway:
	•	Create a REST API and link it to the Lambda function.
	•	Define endpoints for ride booking, user verification, etc.
	5.	AWS Cognito:
	•	Set up a user pool in AWS Cognito.
	•	Configure the pool ID in cognito-auth.js.
	6.	Run Locally:
	•	Open index.html in a browser for the homepage.

Key Features
	1.	User Authentication:
	•	AWS Cognito handles sign-up, sign-in, and user verification.
	•	signin.html and register.html implement these features.
	2.	Ride Booking:
	•	Users can book rides via ride.html.
	•	Rides are processed using Lambda and stored in DynamoDB.
	3.	Mapping:
	•	Real-time location tracking with Mapbox, supported by esri-map.js.
	4.	Investors and Unicorn Features:
	•	Informational pages for branding and additional services.

Testing
	•	Frontend: Open HTML files in a browser and inspect developer console logs.
	•	Lambda: Test locally using lambdaTest.js or the AWS Lambda console.
	•	End-to-End: Use tools like Postman to simulate API calls to API Gateway.

This repo contains the code files used in this [YouTube video](https://youtu.be/K6v6t5z6AsU).



