# aws--project
AWS MINI PROJECT -Email Forwarding SystemUsing Lambda Function in AWS






import json
import boto3

def lambda_handler(event, context):
    bucket_name = "massmailingbucket"
    file_name = "rdlCourseSyllabusNew.pdf"
    
    print("event: ", event)
    print("bucket_name: ", bucket_name)
    print("file_name: ", file_name)
    
    subject = 'Event from' + bucket_name
    
    client = boto3.client("ses")
    
    body =  """
                This is a notification mail sent to inform you about VENKATESH.
                The file {} is inserted into {} bucket_name
            """.format(file_name,bucket_name)
            
    message = {"Subject": {"Data": subject}, "Body": {"Html": {"Data": body}}}
    response = client.send_email(Source = "venkateshkattamuri2005@gmail.com", Destination = {"ToAddresses": ["ramsronyvenky2005@gmail.com"]},Message = message)
    print("The mail has been sent successfully")
