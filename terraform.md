## Create a main.tf file, like this:
```sh
provider "aws" {
  region = "eu-central-1"
}

resource "aws_vpc" "main" {
  id =
  cidr_block       = "10.0.0.0/16"
  instance_tenancy = "dedicated"

  tags {
    Name = "main"
  }
}

resource "aws_security_group" "sg1" {
  name =
  description =
  vpc_id = "${aws_vpc.main.id}"
  ingress {
    from_port =
    to_port =
  }
  egress{
    from_port =
    to_port = 
  }
}
  

resource "aws_instance" "gh1" {
  ami = ""
  instance_type = "t2.large"
  tags {
    Name = "application-server1"
  }
}

resource "aws_instance" "gh2" {
  ami = ""
  instance_type = "t2.large"
  tags {
    Name = "application-server2"
  }
}

resource "aws_instance" "db" {
  ami = ""
  instance_type = "t2.large"
  tags {
    Name = "database-server"
  }
}


resource "aws_elb" "loadbal" {
  name               = "gesundheit-elb"
  availability_zones = ["eu-central-1"]

  access_logs {
    bucket        = "datas3"
    bucket_prefix = "gh"
    interval      = 60
  }

  listener {
    instance_port     = 8000
    instance_protocol = "http"
    lb_port           = 80
    lb_protocol       = "http"
  }

  listener {
    instance_port      = 8000
    instance_protocol  = "http"
    lb_port            = 443
    lb_protocol        = "https"
    ssl_certificate_id = "arn:aws:iam::123456789012:server-certificate/certName"
  }

  health_check {
    healthy_threshold   = 2
    unhealthy_threshold = 2
    timeout             = 3
    target              = "HTTP:8000/"
    interval            = 30
  }

  instances                   = ["${aws_instance.gh1.id}", "${aws_instance.gh2.id}"]
  cross_zone_load_balancing   = true
  idle_timeout                = 400
  connection_draining         = true
  connection_draining_timeout = 400

  tags {
    Name = "gesundheit-terraform-elb"
  }
}
```

#### To execute:
```sh
terraform plan
terraform apply
```
