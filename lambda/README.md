# Lambda Function
- Author : [HunSeol](https//www.github.com/seolhun)
- [Summray](https://github.com/Seolhun/aws#2-lambda)

## [Official Documentation](https://aws.amazon.com/ko/lambda/)

## Lambda Process
- Author > Debug > Test > Author (Simply excuted the function)

1. Event source 
	- S3 (File gets uploaded)
	- Cloud Watch (Scheduled)
	- API Gateway(HTTP Request)

2. Code (Lambda)
	- NodeJS
	- Python
	- Java
	- C#

3. Result
	- Interact with other AWS services
	- `Return Response`

## How it works
1) Create a **root entry file + handler method.** For example an `index.js`  file with the `exports.handler = (event, ...) => { ... }`  method.

If you use a different file name AND/OR different starting handler function, you'll need to adjust your Lambda config! Set Handler to `[FILENAME].[HANDLER-FUNCTION-NAME]`  (default: `index.handler`).

2) You may split your code over multiple files and import them into the root file via `require('file-path')`. This is also how you could include other third-party JavaScript (or other languages) packages.

3) **Select all files and then zip** them into an archive. **Important: DON'T put them into a folder and zip the folder. This will not work!**

4) Upload the created zip file to Lambda ("Code" => "Code entry type" => "Upload a .ZIP file")


## Examples
1. `exports.handler = (event, context, callback) => {}`
	1. event
		- Getting `Reqeust body`.
	2. context
	3. callback

2. If you check the lambda proxy
	- Must have headers, like this.
		```javascript
		exports.handler = (event, context, callback) => {
	    	callback(null, {headers: {'Control-Access-Allow-Origin': '*'}});
		};
		```


## Reference
- [Udemy - AWS Serverless by `Maximilian Schwarzmüller`](https://www.udemy.com/aws-serverless-a-complete-introduction/learn/v4/content)
- [AWS re:Invent 2017](https://www.youtube.com/watch?v=pMyniSCOJdA)
