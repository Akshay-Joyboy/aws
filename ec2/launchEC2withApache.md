## Launching a Linux EC2 Instance and delivering a Simple Login Page

launch ec2 instance 
connect to the ec2 instance 

```bash
sudo yum install httpd -y
```
Switch to 
```bash
cd /var/www/html
```
### create a file index.html
```bash
vim index.html
```
####press 'i' to insert mode 

#### Add your code 
```bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="container">
        <form class="login-form">
            <h2>Login</h2>
            <div class="input-group">
                <label for="username">Username</label>
                <input type="text" id="username" name="username" required>
            </div>
            <div class="input-group">
                <label for="password">Password</label>
                <input type="password" id="password" name="password" required>
            </div>
            <button type="submit">Login</button>
            <p class="signup">Don't have an account? <a href="#">Sign up</a></p>
        </form>
    </div>
</body>
</html>
```
## press esc and then :wq

to write and quit

next

### create another file styles.css
```bash
* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.container {
    background-color: #ffffff;
    padding: 40px; /* Increased padding */
    border-radius: 8px;
    box-shadow: 0 2px 20px rgba(0, 0, 0, 0.15); /* Increased shadow for depth */
    width: 400px; /* Set a fixed width */
}

.login-form {
    display: flex;
    flex-direction: column;
}

h2 {
    margin-bottom: 30px; /* Increased margin */
    text-align: center;
    font-size: 24px; /* Larger heading */
}

.input-group {
    margin-bottom: 20px; /* Increased margin */
}

label {
    margin-bottom: 8px; /* Increased margin */
    font-weight: bold;
}

input[type="text"],
input[type="password"] {
    padding: 15px; /* Increased padding */
    border: 1px solid #ccc;
    border-radius: 4px;
    width: 100%;
    font-size: 16px; /* Larger font size */
}

button {
    padding: 15px; /* Increased padding */
    background-color: #007BFF;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 16px; /* Larger font size */
}

button:hover {
    background-color: #0056b3;
}

.signup {
    margin-top: 20px; /* Increased margin */
    text-align: center;
}

.signup a {
    color: #007BFF;
    text-decoration: none;
}

.signup a:hover {
    text-decoration: underline;
}
```
Run the following command to start the Apache service:

```bash
sudo systemctl start httpd
```
OR

```bash
sudo service httpd start
```

To enable it to start on boot, run:
```bash
sudo systemctl enable httpd
```
OR

```bash
service httpd on
```
To check the status of the service:
```bash
systemctl status httpd
```
OR

```bash
service httpd status
```
now copy the publicIPv4 address of your instance and paste it in your broswer
