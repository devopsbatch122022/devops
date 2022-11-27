
#### Provider Details
```
provider "aws" {
  region     = "us-west-2"
  access_key = "my-access-key"
  secret_key = "my-secret-key"
}

```

#### ++++++++++++  Addition  +++++++++++++++

#### EC2 DETAILS
```
provider "aws" {
  region     = "us-west-2"
  access_key = "my-access-key"
  secret_key = "my-secret-key"
}


resource "aws_instance" "web_server" {
  ami           = "ami-id"
  instance_type = "type"
  key_name      = "key-without-pem-extention"
  vpc_security_group_ids = ["sg-id"]

  tags = {
    Name = "my-web_server"
  }
}
```
