---
title: "AWS IAM policy for only one region"
categories: ["aws", "iam"]
---
 
## Problem
You want to create IAM policy that will allow access to only one region.
 
## Solution
You can use `Condition` to specify that only one region is allowed:
 
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "*",
      "Resource": "*",
      "Condition": {
        "StringEquals": {
          "aws:RequestedRegion": "eu-west-1"
        }
      }
    },
    {
      "Effect": "Deny",
      "Action": ["iam:PassRole", "iam:CreateServiceLinkedRole"],
      "Resource": "*"
    }
  ]
}
```