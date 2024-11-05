---
title: "Terraform: An Effective Hello World"
date: 2024-05-06T19:40:42-06:00
tags:
  - Development
  - DevOps
  - Terraform
categories:
  - Ingenieria
languages:
  - en
images: imagenes/2024/06/tf-hello-world.png
caption: Midjourney prompt "Terraform a world of DevOps CI and CD"
paragraphs: Long ago, I wanted to dive into the world of Terraform, and finally, I did. Here are my notes on this "hello world" experience.
---

I stumbled upon Anton's videos[^1] almost a year ago. I particularly enjoyed the benchmarking series where different languages or frameworks competed against each other. [This video on Terraform](https://www.youtube.com/watch?v=6XSroskdCF0) caught my attention, but I hadn't found the time to get my hands dirty.

As a tech generalist, I'm often drawn to new frameworks or languages, and infrastructure as code was no exception. My last encounter with infrastructure was during college, working with Vagrant and VM administration, which was some years ago.

Though I missed the DevOps wave initially, I still intend to give it a try at some point in my career. Having a clear tutorial that's easy to follow is a great help.

## Coverage

I won't lie; I have some gaps in my knowledge, but here's what this introduction to Terraform covers:

- Setting up an AWS account (Easy)
- Installing Terraform (Super easy)
- Creating a single web server with Terraform (Hard)
- Implementing auto-scaling of your infrastructure with infrastructure as code (Very hard)

## First Steps

Creating an account and installing the software are relatively easy at this point.

> A credit card is required, but Amazon will not charge anything, and you can do a lot with the capabilities of the free tier.

## Doing Cool Stuff

The code can be found on my GitHub account. Let's discuss this section of code:

```terraform
resource "aws_instance" "example" {
  ami               = "ami-09040d770ffe2224f"
  instance_type     = "t2.micro"

  vpc_security_group_ids = [ aws_security_group.instance.id ]

  user_data         = <<-EOF
                    #!/bin/bash
                    echo "Hello, World" > index.html
                    nohup busybox httpd -f -p ${var.server_port} &
                    EOF

  user_data_replace_on_change = true

  tags = {
    Name = "Example"
  }
}
```

How many lines of code are here? That's all you need to launch a web server and kickstart your journey with Terraform. Short and deterministic — an effective "hello world."

## The Missing Gaps of Knowledge

For the second part of this tutorial, you'll be creating an ALB (Application Load Balancer), security groups, and health checks.

There's some magic behind the scenes; AWS creates a VPC by default, so you don't have to create one (for example purposes, but production is another thing).

Topics to study further:

- Security groups, I have no idea what I'm doing here 😅
- AWS VPC by default, how does this VPC work, and what should be done for production environments?

## Conclusion

I thoroughly enjoyed this tutorial and exploring Terraform with this broad overview. I'm eager to try more with Terraform.

[^1]: [YouTube @AntonPutra](https://www.youtube.com/@AntonPutra)

