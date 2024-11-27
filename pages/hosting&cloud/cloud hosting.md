# serverless
Check out [this explanation](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://www.cloudflare.com/learning/serverless/what-is-serverless/&ved=2ahUKEwjujPeuqO2JAxXHe6QEHcYyMt8QFnoECBMQAQ&usg=AOvVaw3Iz5rmWJ_8gwqpiOUIVPvr) from CloudFlare
## Definition
Serverless computing refers to a ***cloud computing execution model*** where cloud providers ***automatically manage the infrastructure***. The ***developer*** only needs to ***write code***, ***upload*** it, and the provider takes care of scaling, availability, and fault tolerance.
## Benefits of Serverless
- ***Reduced complexity***: Serverless eliminates the need to manage servers, load balancing, and scaling.
- ***Cost efficiency***: You pay only for the compute resources that your code actually uses, rather than pre-allocating resources.
- ***Automatic scaling***: The cloud provider handles scaling based on demand, without the need for manual configuration.
## Common Use Cases
Serverless is often used in ***microservices*** architectures, ***API*** backends, real-time ***file processing***, and ***event-driven functions*** (like image resizing or data transformation).
## Cloudflare Workers as an Example
Cloudflare Workers are an example of serverless solutions, allowing developers to run JavaScript, Rust, and other languages closer to the user (at the network edge). This improves performance and reduces latency.
## Challenges
While serverless offers many benefits, there are some challenges, such as handling stateful applications, potential vendor lock-in, and the complexity of debugging and monitoring serverless functions.
![[Pasted image 20241121122329.png]]
# AWS Lambda
this is a quick tutorial to test AWS Lambda with `lambda_handler` function creating `myfirstfunction` app.
## steps
- create a new python function from scratch
- test editing `lambda_handler` function by adding a print (e.g. `print("Hello lambda!")`)
- click `Test` to create a new test event based on `hello world` model event
- run `Test` with created model event
- with ***eventbridge*** create an event that runs `myfirstfunction` every 5 minutes
- check on ***lambda*** the periodic invocations.
- delete