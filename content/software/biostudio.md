---
title: "BioStudio"
featured_image: '/images/bityeast.png'
draft: true
---

# Update for 2023

* We recommend installing as an AWS EC2 instance using our AMI ami-dcb8f4b6 as described in our [supplement from Richardson et al 2017 Science](/files/biostudio_som.pdf).
* Most of the notes below are standard procedures for launching an AWS EMI. The BioStudio-specific notes are highlighted as **BioStudio-specific**.
* Amazon provides a guide to [launching an EC2 instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-launch-instance-wizard.html).
* We recommend an instance with resources equivalent to m5.xlarge or larger and configuring to accept SSH, HTTPS, and HTTP.
* For ease of connecting, we request a public IPV4 address.
* As of Nov 2023, we have had no difficulties launching the instance. Note that our AMI does not support ENA, which restricts the choices of instance type.
* Once the instance is started, if you are using SSH from MacOS you may have to include an option to permit ssh-rsa. Also note that the user name is ``ubuntu`` rather than ``root`` for our instance: ``ssh -i "yourkey.pem" -o PubkeyAcceptedKeyTypes=+ssh-rsa  ubuntu@your.server.address``
* **BioStudio-specific**: The top-level directory has a driver file ``biostudio_design.sh`` that begins by downloading a reference genome from SGD. Unfortunately, the conventions for GFF3 are fluid and the file location on SGD also changes. Therefore we provides this stable version of the [Saccharomyces cerevisiae reference genome GFF3](/gff3/saccharomyces_cerevisiae.gff) for download. We recommending downloading our GFF3 and then using SFTP or SCP to copy it to the AWS instance. Once you have downloaded this GFF3, you can comment out this line in ``biostudio_design.sh``: ``curl -O http://downloads.yeastgenome.org/curation/chromosomal_feature/saccharomyces_cerevisiae.gff``
* **BioStudio-specific**: We have also found that the behavior of a temporary directory required to be writeable by GBrowse may need to be initialized. Check that the directory ``/tmp/bio_graphics_ff_cache_33`` exists with permissions 777. If the directory does not exist, then create it and change the permissions: ``mkdir /tmp/bio_graphics_ff_cache_33; chmod 777 /tmp/bio_graphics_ff_cache_33``
* Read the ``readme`` file in the top directory of the instance and execute the ``biostudio_design.sh`` script -- everything should work!
* If you have problems, contact Joel Bader, joel dot bader at jhu dot edu
