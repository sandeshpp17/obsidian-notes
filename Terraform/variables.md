
in each language its best practice to not hardcode the values.
use variables and store those in file and give the reference in the code. it will make easy to change the values without changing the code itself.

main.tf
```json
resource "local_file" "pet" {
	filename = var.filename
	content = var.content
}
```

variables.tf
```json
variable "filename" {
	default = "/root/pets.txt"
}
variable "content" {
	default = "We love pets!"
}
```

## Different methods of passing variables.

1. **variables.tf** 
```
variable filename {
 type= string
}
```

2. **environment variable**
```
export TF_VAR_filename="/root/cats.txt"
```

3. **terraform.tfvars**
```
filname = "/root/pets.txt"
```

4. **variable.auto.tfvars**
```
filename = "/root/mypet.txt"
```

5. **command line**
```
terraform apply -var "filename=/root/best-pet.txt"
```
## variable priority

| Order | Option                               |
| ----- | ------------------------------------ |
| 1     | env var                              |
| 2     | terraform.tfvars                     |
| 3     | `*.auto.tfvars (alphabetical order)` |
| 4     | -var or -var-file (command line)     |
Command line has highest priority.

## Variable dependencies

when some resources depends on other resource variable output so the variable dependencies are used. like random output generate by resource and that will be used by other resource. dependencies can be used if one resource is dependent on other resource.

```
resource "local_file" "time" {
	filename = "/root/time.txt"
	content = var.time_static.time_update
	depends_on = [time_static.time_update]
}

resource "time_static" "time_update" {
}
```

## variable output

the output of one resource can be use in other resource as a variable. and it can be shown at terraform apply

```
resource "local_file" "welcome" {
	filename = "/root/time.txt"
	content = "Welcome"
}

output "name" "welcome_message" {
	value = local_file.welcome.content
}

```

