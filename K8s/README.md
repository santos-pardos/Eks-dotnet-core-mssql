## EKS Secret
kubectl create secret generic mssql-secret --from-literal=SA_PASSWORD="CorrectHorseBatteryStapleFor$"


## Secrets
echo -n "CorrectHorseBatteryStapleFor$" | base64                                                                                                                           
Q29ycmVjdEhvcnNlQmF0dGVyeVN0YXBsZUZvciQ=
