# AWS-CLI EC2 APACHE Web Server
[Quelle](https://towardsaws.com/how-to-use-aws-cli-to-launch-an-ec2-web-server-with-apache-9c20d07e07be)

### Cloud9 mit Github per SSH verbinden/vernküpfen

### Projekt erstellen

#### Projektverzeichnis erstellen

    mkdir AWS_CLI

#### Textdatei für Ressourcen erstellen 

    touch ressources.txt

#### Überprüfen AMI

    aws ec2 describe-images --owners amazon --filters "Name=name, Values=amzn2-ami-hvm-2.0.????????.?-x86_64-gp2" "Name=state, Values=available" --query "reverse(sort_by(Images, &Name))[:1].ImageId" --output text

#### Erstellen Key Paar für Projekt

    aws ec2 create-key-pair --key-name Zwick_Apache --query 'KeyMaterial' --output text > Zwick_Apache.pem
    

#### Überprüfen

    ls -lah
    
#### Beschreibung von KeyPar

    aws ec2 describe-key-pairs --key-name Zwick_Apache
    
#### Security-Group erstellen

    aws ec2 create-security-group --group-name Zwick_Apache_SG --description "Allows SSH, HTTP and HTTPS connections for Web Server"
    
#### Security-Gruppe-ID

    sg-0b581b521dadb1c92
    
#### Regeln zur Security-Gruppe hinzufügen

#### Port 22

    aws ec2 authorize-security-group-ingress --group-id sg-0b581b521dadb1c92 --protocol tcp --port 22 --cidr 0.0.0.0/0
    
#### Port 80

    aws ec2 authorize-security-group-ingress --group-id sg-0b581b521dadb1c92 --protocol tcp --port 80 --cidr 0.0.0.0/0
    
#### Port 443

    aws ec2 authorize-security-group-ingress --group-id sg-0b581b521dadb1c92 --protocol tcp --port 443 --cidr 0.0.0.0/0

#### Überprüfen der SG-Regeln

    aws ec2 describe-security-groups --group-ids sg-0b581b521dadb1c92 --output table
    
#### Erstellen Bash Script Datei (webscript.sh)

    touch webscript.sh
    
#### Erstellen einer EC2-Instanz mit folgendem Befehl

    aws ec2 run-instances --image-id  --count 1 --instance-type t2.micro --key-name NVirKeyPair --security-group-ids sg-0b581b521dadb1c92 --user-data file://webscript.sh