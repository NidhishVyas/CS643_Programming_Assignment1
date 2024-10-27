# AWS EC2 Java Project - Object and Text Detection

This project demonstrates how to set up and run object and text detection Java programs on AWS EC2 instances. It covers configuring AWS credentials, launching EC2 instances, setting up the necessary environment, and executing Java applications for object and text detection.

## Prerequisites

### Configure AWS Credentials
1. **Copy Credentials:**
   - Obtain your `AWS access_key`, `secret_key`, and `session_token` from **AWS Details**.
   - Note: These credentials are temporary and will expire every 3 hours or after a session reset.

2. **Add Credentials to AWS Config:**
   - Open the `~/.aws/credentials` file and add your credentials in the following format:
     ```plaintext
     [default]
     aws_access_key_id = YOUR_ACCESS_KEY
     aws_secret_access_key = YOUR_SECRET_KEY
     aws_session_token = YOUR_SESSION_TOKEN
     ```

3. **Download PEM File:**
   - Download the PEM file from AWS for SSH access to EC2 instances.

## Step 1: Launch EC2 Instances

1. **Navigate to EC2 Dashboard:**
   - Go to **EC2 Dashboard** → **Launch Instance**.

2. **Select Amazon Linux 2 AMI:**
   - Choose **Amazon Linux 2 AMI (HVM)** with `t2.micro` instance type.

3. **Name the Instances:**
   - Name your instances (e.g., **EC2-A** for object detection and **EC2-B** for text detection).

4. **Configure Key Pair:**
   - Select `Create New Key Pair`, download it, and keep it safe for SSH access.

5. **Set Network Security:**
   - Create a security group allowing:
     - **SSH** traffic for secure access.
     - **HTTP/HTTPS** (if required).
   - Set the source type to **My IP** for **Anywhere**.

6. **Storage and Advanced Details:**
   - Leave as default.

## Step 2: SSH into EC2 Instances

Use the following command to SSH into each instance:

```bash
ssh -i "path-to-key.pem" ec2-user@public-ip
```

- Replace `path-to-key.pem` with the location of your PEM file and `public-ip` with the EC2 instance’s public IP.

## Step 3: Set Up Java and Maven

1. **Install Java:**
   ```bash
   sudo yum install java-1.8.0-openjdk -y
   ```

2. **Install Maven:**
   ```bash
   sudo yum install maven -y
   ```

## Step 4: Create Java Project Structure with Maven

1. **Generate Project Structure:**
   - Use Maven to generate the project structure:

     ```bash
     mvn archetype:generate \
         -DgroupId=com.example \
         -DartifactId=my-java-project \
         -DarchetypeArtifactId=maven-archetype-quickstart \
         -DinteractiveMode=false
     ```

2. **Build and Package the Project:**
   - Navigate to your project directory and run:

     ```bash
     mvn clean package
     ```

3. **Run the Java Program:**
   - Execute the generated JAR file:

     ```bash
     java -jar target/my-java-project-1.0-SNAPSHOT.jar
     ```

## Step 5: Running Detection Programs

### Running Object Detection on EC2-A

1. **Execute Object Detection Program:**
   ```bash
   java -jar AWSObjectDetection.jar
   ```

2. **Verify Output:**
   - The object detection results will appear in the terminal.
   - You can retrieve additional results by checking the AWS Console and using the "Polling for Messages" option.

### Running Text Detection on EC2-B

1. **Execute Text Detection Program:**
   ```bash
   java -jar AWSTextRekognition.jar > output.txt
   ```

2. **Check Output:**
   - View `output.txt` for detected text output.
   - Verify any generated queues or data in the AWS Console.

## Screenshots

### Object Detection Output
![Object Detection](./Screenshot%201.png)

### Queue Results in AWS Console
![Queue Result](./Screenshot%20SQS.png)
![Queue Result](./SQS%20Messages.png)

### Text Detection Output
![Text Detection](./Screenshot%202.png)


## Notes
- **Temporary Credentials**: AWS credentials will expire every 3 hours.
- **Security**: Limit SSH and HTTP/HTTPS access to your IP for enhanced security.

This guide covers essential steps for setting up and running Java-based object and text detection programs on AWS EC2 instances.
