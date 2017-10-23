# Architecture could also use AWS ECS

#### this is how we would create AWS ECS resources using terraform:
```sh
resource "aws_ecs_cluster" "gh_ecs_cluster" {
   name = "example-cluster"
}

resource "aws_autoscaling_group" "ecs_cluster_instances" {
  name = " "
  min_size = " "
  max_size = " "
  launch_configuration = "${aws_launch_configuration.ecs_instance.name}"
}

resource "aws_launch_configuration" "ecs_instance" {
  name = ""
  instance_type = " "
  image_id = " "
  load 
}

resource "aws_elb" "gh_elb" {
  name =
  listener {
  }
}

resource "aws_ecs_service" "s1_service" {
  family =
  cluster =
  task_definition = 
  desired_count =
  load_balancer {
    elb_name =
   }
 }

resource "aws_ecs_task_definition" "s1_task" {
  container_definitions =<<EOF
 [{
   "name":
   "image": "khushboo30/s1:v1.0.0",
   "cpu":
   "memory":
   "portMappings": [{ "container_port":"5000", "host_port":"5000" }]
  }]
