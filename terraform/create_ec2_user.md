
#### Provider Details
```
provider "aws" {
  region     = "us-west-2"
  access_key = "my-access-key"
  secret_key = "my-secret-key"
}
```

```
$ terraform init
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
}
```

#### EC2 DETAILS  (key_name)
```
provider "aws" {
  region     = "us-west-2"
  access_key = "my-access-key"
  secret_key = "my-secret-key"
}


resource "aws_instance" "web_server" {
  ami           = "ami-id"
  instance_type = "type"
  key_name      = "key-without-pem-extention"               ## Addition
}
```


#### EC2 DETAILS  (security_group)
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
  vpc_security_group_ids = ["sg-id"]                      ## Addition
}
```

#### EC2 DETAILS  (tags)
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

  tags = {                                                ## Addition
    Name = "my-web_server"
  }
}
```


```
$ terraform init
$ terraform plan
$ terraform apply              ## -auto-approve
$ terraform destroy            ## -auto-approve
```
