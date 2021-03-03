

# ................... 100 Terraform Interview Questions  ....................

## By  Mamun Rashid :: https://www.linkedin.com/in/mamunrashid/

### Last Updated: 2021.03.03
###
###

*  ( I also have 275 Multiple Choice Questions for Hashicorp Terraform Associate Certification Exam found at the link below:
*    https://testmoz.com/1245195 )

*  ( Mr. Bachina has also made an execllent set, which is very effective, as well found at the link below:
*    here: https://medium.com/bb-tutorials-and-thoughts/250-practice-questions-for-terraform-associate-certification-7a3ccebe6a1a )

##
##

#### 1. Imagine that there are 20 people in the company who use Terraform that manages resources in AWS or GCP. How can you set up a system that tackles that? What could be the issues that can arise from this?


######   Answer: 
######   At least two issues arise when multiple people work on Terraform together touching the same resources:
######          1. state file overrides
######           2. code overrides
######
######           State file overrides can be solved using remote states
######           Code overroides can be solved usig git repos and branching strategies.

##
#### 2. There are 5 people in your team that use Terraform. Some time in the last few days, a resource in AWS changed. How can you find out who did this?

#####   Answer: If it was done via Console, Cloudtrail can tell you.
#####           If it was done via Terraform code, git repo AND AWS Cloudtrail can tell you.


##
#### 3. You made a module. One Terraform code uses that module. But, now, you improved that module, but the "caller" code is not compatible with the new version of the module.  How can you have both versions of the module in use?

#####   Answer: You can have verions on your modules and the caller code can refer to specific version of the module.


##
#### 4. You have existing infrastructure in AWS that was NOT made by Terraform. How can you bring that infrastructure in Terraform code's control?

#####   Answer: If you all want is the "state" to be in Terraform, you can use "terraform import" commnad.
#####           If you also want terraform code be made, you can either do yourself (until code and state match exactly), or you can use a opensource tool named "Terraformer"

##
#### 5. If N people are using Terraform, How can we make sure people don't bring up resources in AWS/GCP that are too expensive?

#####   Answer: There is proprietory tool call called Scalr. Or, you can use Terraform Enterprise. There may also be a way using Open Policy Agent. Cloud providers often provide tools for this, as well.


6. How can you tackle secrets in Terraform?

   Answer: Starting version 0.14, you can mark your variables "sensitive". This allows logs of these variables to be masked.
           You can also integrate Vault with Terraform.


7. What is the big deal about Terraform v0.13 and above?

   Answer: Before version 0.13, programming logic was nearly impossible to implement in HCL. With 0.13, it is still not super easy, but a huge progress was made.
           There were many other major features released as well (e.g. json output)


8. You have 2 folders of terraform code. Folder A and Folder B. Folder B needs to use output (state) from folder A to create resources. How can you accomplish this?

   Answer: This has been long-standing problem with Terraform. Terragrunt is one way to get this done. Others have implement custom Python scripts that copies states
           back and forthe between folders.


9. Why would you need "data" resources in Terraform?

   Answer: To refer to resources that already exists  in AWS. For example, list of AMIs in a region.


10. Is it safe to store terraform state in a private git repo? Why or why not?

   Answer: It is NOT safe to store in git repos, because it can hold secrets. Also, it is likely that people will override each other's changes in state.


11. If you are tagged to implement Terraform in a team or company where they have never used Terraform, what issues might you solve pre-emptively?

   Answers: Set standars and best practices before you start coding. Also, you many want to import existing resources in Terraform before you start.


12. You are going to deploy similar resources in Development, Staging and Prod environments. How can you code so that you can deploy to similar Terraform code with repeating your code.

   Answer: Hav eno hard-coded variables and use .tfvars file per environment.


13. How would you implement a Terraform pipeline?

   Answer: In the same folder where I have terraform files, I would have .gitlabci.yml file which will have various stages (e.g. tfsec, tflint, checkov, terraform validate, 
             terrform plan and terarform apply and possibly some testing stages).


14. Tell me about a project or task that you did in Terraform?

    Answer: Tell your story.


15.  How do you import state from GCP or AWS?

    Answer: Using terraform import command. Format for each resource type may vary. Once you have successfully imported the state, you can also write terraform code to match
             the state so much your code and state and infrasture are all in sync.


16. Is there a tool for looking into many resources (> 100) in GCP or AWS and automatically made Terraform code for them?

    Answer: Terraformer, (an open source tool). It is magical.


18.  How do you define "backend" in Terraform?

    Answer:  This is directly from Hashicorp Web Site:

             Backends are configured with a nested backend block within the top-level terraform block:


              terraform {
                backend "remote" {
                  organization = "example_corp"
              
                  workspaces {
                    name = "my-app-prod"
                  }
                }
              }


19. What is a provider and why do you need it?

    Answer: Terraform doesn't directly create resources in the cloud. It interacts with provider (given by AWS, GCP, etc.), which enables communication 
            between Terraform and the cloud provider APIs (AWS, GCP etc.).

            Using the same idea, Terraform can also deploy resources in non-cloud applications as long as it has a provider (e.g. Hashicorp Vault) 

20.  Examples of a data resource in AWS?

     Answer: AMIs, aws_instance
             Please see:  https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/instance


21.  When you run your Terraform code on local, how does it get access to your AWS / GCP account?

     Answer: There are couple of ways, but one way is using variables:

              AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY 


22. Can you mark a variable a "secret" such that it does not show up in logs etc?

    Answer: Yes from version 0.14


23. You made Terraform state using v 0.13. Can you modify it using version 0.12?

   Answer: NO.   But, this is possible from 0.14 and up.


24. Can Terraform use Bash environment variables?

   Answer: Yes, mostly. 
           Please see here:
           https://stackoverflow.com/questions/53330060/can-terraform-use-bash-environment-variables


25. Can a module call another module?

   Answer: Yes, it is not recommended


26. Why do we need terraform.tfvars file?

   Answer: If you do not hard code variables, you can set values in terraform.tfvars files (different values per environment).
           This way, your code doesn't change and you can follow DRY principle.


27. If you were to design terraform code for making AWS Security Groups, how would you do it?

  Answer: This one is bit complicated because Secuirty Groups are made up of Secrutiy Group Rules. So, there are two ways you can go about this:
          A. Made a module for SG Rules. A template would call that module N times to build a SG.
          B. 0.13 can take .csv file as input. You can use that to build SG as a List of Maps.


28. Which folder caches module codes locally?

  Answer: .terraform


29. What negative impact does it have if you remove .terraform folder?

  Answer: None. Terraform will simply download everything when you run terraform init command


30. You have the same tf code. WIth the same code, you want to deploy to N environments (states) and be able switch between them. How?

  Answer: Use different .tfvars file for each environment


31. How can you pass csv an argument to a module?

  Answer:  Use csvdecode function. That will read a csv file into a List of Maps. You can pass that directly to a module that accepts List of Maps (One input Variable)
           Please see here for more info on csvdecode:
           https://www.terraform.io/docs/language/functions/csvdecode.html


32. Does Terraform have built-in functions?

  Answer: Yes. Many. e.g. csvdecode.


33. What does "terraform refresh do"?

  Answer: terraform refresh reads the local state and goes back to the cloud and finds drift.
          More info here:
          https://stackoverflow.com/questions/42628660/what-does-terraform-refresh-really-do

34. You have added some new codes in the outputs.tf file (added more things to output). That is the only thing you have added. What command can you now run
      so that you get to see the results even though no change has happened in any other code or any resources in the cloud?

  Answer: terraform refresh


35. What does "terraform taint" do?

  Answer: It artifically marks a resource as "bad". So, next time you run terraform plan, you will try and re-create the resource regardless if the resource has been 
          modified or not. This is a good way to force immutability.

34. How can you get a list of Terraform resources of a given folder with terraform code?

    Answer: terraform state list

35. Can you move terraform state from one place to another?

    Answer: terraform state mv  ......


36. Can you remove JUST 1 item from your "state"? How?

    Answer: terraform state rm

37. Using Terraform , you have deployed 6 resources in AWS. However, a developer deleted on of them via AWS Console. Turns out that , that resource was not needed
     any way. How can you make your terraform code and terraform state sync up now?

    Answer: 1. terraform state rm resource_name &
            2. remove the relevant part of the code that creates the deleted resource


38. What if you do not want terraform apply to ask for your permission before deploying resources?

    Answer: terraform apply --auto-approve


39. Generally speaking, using --auto-approve is bad idea. Can you imagine a situation where , it may ok ?

    Answer: In development environments


40. Examples of other data resources that are part of AWS provider:

    Answer:
      "aws_acm_certificate"
      "aws_api_gateway_account"
      "aws_codecommit_repository" on and on and on

41. How does terraform get access to AWS?

    Answer: Using variable in aws provider section

    provider "aws" {
        access_key = "<AWS_ACCESS_KEY>"
        secret_key = "<AWS_SECRET_KEY>"
        region = "<AWS_REGION>"
    }


42. How would switch between versions of Terraform?

    Answer:
      mac brew install tfenv
      tfenv (switches between many versions super easily.)

      There are other ways , as well (e.g. using containers and aliases)


43. Scenario Question: Your terraform code, state and cloud resources are all sync.
    Now, you run: terraform state rm foo (foo is one of resources). What will happen now,
    if you run "terraform plan" ?

    Answer: It will say that , it needs to add the resource "foo"


44. What is good command to make your terraform code presentable?

    Answer: terraform fmt


45. What does terraform init command do?

    Answer: Pulls in any refernced modules , among other things.


46. Is there a linting tool for Terraform?

    Answer: Yes. tflint (open source)


47. Is there a tool that can look for security vulnerabilities in your terraform code?

    Answer: Yes. tfsec


48. Does "providers" have versions too?

    Answer: Yes!


49. How do you make sure your code is using a particular version of a provider?

    Answer: In the provider block, you set the version.

      Here is an example from Hashicorp web site:


    provider "aws" {
      version = "~> 1.0"
      access_key = "foo"
      secret_key = "bar"
      region     = "us-east-1"
    }


50. How do you upgrade the version or providers and plugins and modules?


    Answer: terraform init -upgrade


51. What is Interpolation ?

   Answer: Basically using variables.
           0.12 or below, you can use funny $ { } syntax.
           0.13 or above, much more user-friendly

52. How can you make Lambda functions using Terraform?

   Answer:
       Lambda codes live in a folder called src and zip file is created on the fly by 
       terraform (when terraform apply runs) and terraform apply will also use the zip 
       file to deploy lambda function to AWS.


53. If you 10 different .tf files in a folder, in what order does Terraform 
    execute the code?

    Answer: Order is irrelevant. Terraform makes map based on all the .tf files and 
            executed based on that plan, not sequentially.


54. You have mades changes to your code. You did not run terraform plan. You now run
    terraform apply. What will happen?

    Answer: terraform will run terraform plan anyway before running terraform apply

55. Besides terraform.tfvars file, which other files does terraform load for variable values?

    Answer: *.auto.tfvars


56. You are building ec2 machines via terraform. However, you also have to install 
    software and configurations on these ec2 machines. How can you do this using Terraform?

    Answer: There are multiple ways. One way is to use user-data scripts.

57. How to create ssh key using terraform:

  ans:  Terraform can generate SSL/SSH private keys using the tls_private_key

58.  How can you do "if-then-else" logic in Terraform version 0.13 and above?
     

     Answer: (Directly from terraform pages:)

      A common use of conditional expressions is to define defaults to replace invalid values:
         var.a != "" ? var.a : "default-a"
         If var.a is an empty string then the result is "default-a", but otherwise it is the actual value of var.a.


59. What is "Dynamic Block" in Terraform?

    Answer: It is kind of like a for loop.


60. During terraform plan , a resource is successful  (i.e. there are no issues with terraform plan), 
    but fails during provisioning (i.e. during "apply") , what happens to the resource in terraform state?

    Answer: It is marked as "tainted"

61. If a provider needs to download data, in which phase does it happen?

    Answer: terraform plan


62. In "terraform" block , how to do you make sure that user is using terraform version 0.11 or above?

    Answer:

    terraform { required_version = "~> 0.11" } 


63.  Do Plugins execute as separate processes?

     Answer: Yes.


64. What is the difference between provideer and a plugin?

    Answer: It is kind of same, but not :-)
      Best answer is given here:
      https://stackoverflow.com/questions/63440271/understanding-terraform-provider-and-plugin


65. As best practice and code readibility, you should always have ___________ file?

    Answer: main.tf  (For the reader of your code, this is the entrypoint)


66. You have code for resource A and resource B in your main.tf . However, you do not want resource B created until resource A
    is created.  How do you accomplish this?

    Answer: In the block for resource B, add a depends_on parameter.


67. Can you use filter inside a data block?

    Answer: Yes.


68. Which will tell terraform to look for all module source lines and retrieves the module codes and report errors if can't find them ?

    Answer: terraform get


69. What is a terraform provisioner?

    Answer: (straight from Hashicorp documentation):

      Provisioners are used to execute scripts on a local or remote machine as part of resource creation or destruction. 
      Provisioners can be used to bootstrap a resource, cleanup before destroy, run configuration management, etc. 


70. Examples of provisioners:

    Answer: local-exec , remote-exec


71. What is a null resource?

    Answer: It is a thing runs through the resource life-cycle, but actually does nothing.


72. If a null resource takes no action, what could possibly a use case for it?

    Answer: null resource has a magic parameter called "triggers". Any change in the triggers, makes the null-resource run its resource
            cycle again.


            Here is example from:  https://blog.logrocket.com/dirty-terraform-hacks/

            variable "config_path" {
              description = "path to a kubernetes config file"
            }
            variable "k8s_yaml" {
              description = "path to a kubernetes yaml file to apply"
            }

            resource "null_resource" "kubectl_apply" {
              triggers = {
                config_contents = filemd5(var.config_path)
                k8s_yaml_contents = filemd5(var.k8s_yaml)
              }

              provisioner "local-exec" {
                command = "kubectl apply --kubeconfig ${var.config_path} -f ${var.k8s_yaml}"
              }
            }


            In the above example, any changes to the contents of the Kubernetes config file or Kubernetes YAML will cause the command to rerun.


73. You want to run terraform plan. However, you want to point to a non-default state file. How?

    Answer: -state=PATH



74. True or False: Providers and provisioners are both provided via plugins.

    Answer: True


75. Can terraform handle map type variable natively?

    Answer: Yes


76.  A ________ type is a type that groups multiple values into a single value.


    Answer: Complex


77.  Launch interactive console via which command?

    Answer: terraform console


78.  If you want 2 identical aws provider sections, then you have use :

     Answer:  alias keyword on the 2nd one.


79. Can plugins vary folder by folder?


    Answer: plugins for each terraform code folder are independent of each other.



80. You have file foo.tf with 5 resources defined in it. You also bar.tf with another 5 resources defined in it. 
    If you concatenate the 2 files and deleted foo.tf bar.tf files, what would be the impact?

    Answer: nothing


81. State file is always encrypted at rest. True or False:

    Answer: False


83. If you have chosen S3 as your backend for state files. What's easiest way to make sure state file(s) are encrypted at rest?


    Answer: Just make the bucket encrypted


84. _________ command creates a visual graph of Terraform resources:


    Answer: terraform graph


85. What allows terraform users to apply policy as code to enforce standardized configurations for resources being deployed?


    Answer: Sentinel


86. When terraform init downloads plugins, where does it save it?


    Answer: .terraform.d folder


87. Where is local copy of the modules saved?


    Answer: .terraform folder


88. Which file keeps a local copy of the "state" (if remote state is not used) ?


    Answer: terraform.tfstate


89. Have you noticed any change with respect to error handling beginning version 0.13?


    Answer: Yes. It is LOT better. For example, it points to file name and line numbers very accurately (where the problem is). 
            Also, error messages , in general, are significantly clearer.


90. Every Terraform resource has a meta-parameter you can use for iteration called _________ .


    Answer: index


91. Scenario Question: You wrote some terraform code. You ran plan and apply and resources got created. Then, you ran terraform destroy and resources got
      destroyed. What happens if you now run "terraform plan" ?


    Answer: It will say that it needs to re-create the same resources again.


92. Is Terraform idempotent?


   Answer: Yes


93. What does "root module" mean?


    Answer: It's the folder that may or may not call other child modules , but no other code calls this folder as a module.


94. Why is root module called a "module" when its just a folder?


    Answer: Because, any folder can be used as a child module. For example, if you have codes in folder A, you can call it from folder B,
              as if folder A is a module.


95.  When you run "terraform plan", if there are no syntax error, you will get what at the bottom of the output?


     Answer: Number of sources to be created, modified, and destroyed


96. Is there way to validate your terraform code syntax, before running terraform plan?


    Answer: Yes. "terraform validate"


97. Is there way to automatically create a Readme.md file based on your terraform code?


    Answer:  terraform-docs markdown . >> README.md
      terraform-docs is an open source tool. You can find it here:
      https://github.com/terraform-docs/terraform-docs  
    

98. Persistence data stored in state for a particular environment is called?

    
    Answer: workspace


99. Which workspace do you work in by default?


    Answer: default


100. How do you know which workspaces you have in the first place?


    Answer: terraform workspace list


             

                                       Terraform Interview Questions

                                               Mamun Rashid

                                   https://www.linkedin.com/in/mamunrashid/

