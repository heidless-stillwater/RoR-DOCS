
## [Cloud SQL(MySQL, PostgreSQL and Microsoft SQL Server) automatically backup and stores into the GCS bucket](https://medium.com/google-cloud/cloud-sql-mysql-postgresql-and-microsoft-sql-server-automatically-backup-and-stores-into-the-gcs-d01cf3677c67)


##################################################################################
##################################################################################

```
gcloud init


echo '######################'
echo 'set ENV'
source config/.env-vars

cd ./BACKUPS/<BACKUP DIR>
source ../../config/.env-vars
echo '######################'

```

## set SERVICE ACCOUNT Permissons
```
echo 'SET PERMISSIONS - objectAdmin & legacyBucketWriter'
--
# set permissoons on INSTANCE service account
export SQL_SVC_ACC=`gcloud sql instances describe ${GCP_INSTANCE} | grep serviceAccountEmailAddress`
echo $SQL_SVC_ACC

--
serviceAccountEmailAddress: p32685880208-vg0u6f@gcp-sa-cloud-sql.iam.gserviceaccount.com 

--
#############################
# assing Svc Account
export DB_SVC_ACCOUNT=p32685880208-vg0u6f@gcp-sa-cloud-sql.iam.gserviceaccount.com

# set PERMISSION on Svc Account
gsutil iam ch serviceAccount:${DB_SVC_ACCOUNT}:objectAdmin gs://${GCP_BUCKET}
gsutil iam ch serviceAccount:{DB_SVC_ACCOUNT}:legacyBucketWriter gs://${GCP_BUCKET}
#############################

```

```

echo '######################'
echo 'set ENV'
source config/.env-vars

cd ./BACKUPS/<BACKUP DIR>
source ../../config/.env-vars
echo '######################'

#############
# Take Backup
#
timestamp=`date +%s`
MSG=2nd-DRAFT

echo PROJECT: $GCP_PROJECT
echo INSTANCE: $GCP_INSTANCE
echo DB: $GCP_DB_NAME
echo USER: $GCP_DB_USER
echo BUCKET: $GCP_BUCKET

export BK_COMMENT='image-test-0'
echo COMMENT: $BK_COMMENT

export BK_TIMESTAMP=`date +%s`
echo TIMESTAMP: $BK_TIMESTAMP

export GCP_FILE=${GCP_INSTANCE}-${GCP_DB_NAME}-${BK_COMMENT}-${BK_TIMESTAMP}.gz
echo FILE: ${GCP_FILE}

echo " "

echo '######################'
echo 'BACKUP DB'
echo $GCP_INSTANCE
echo $GCP_BUCKET
echo $GCP_FILE
echo $GCP_DB_NAME
echo ' '
gcloud sql export sql ${GCP_INSTANCE} gs://${GCP_BUCKET}/backups/${GCP_FILE}    \
--database=${GCP_DB_NAME}	 \
--offload


#################
# DOWNLOAD BACKUP
# cd <BACKUP DIR>

echo $GCP_BUCKET
echo $GCP_FILE
gcloud storage cp gs://${GCP_BUCKET}/backups/${GCP_FILE} .


##############
# RE-CREATE DB
#
echo 're-create DB'
echo $GCP_DB_NAME
echo $GCP_INSTANCE
echo ' '
gcloud sql databases delete $GCP_DB_NAME \
    --instance $GCP_INSTANCE

gcloud sql databases create $GCP_DB_NAME \
    --instance $GCP_INSTANCE


###############
# UPLOAD BACKUP
#
#GCP_FILE=alpha-blog-0-instance-0-alpha-blog-0-db-0-LatestSnapshot-1718973507.gz 

echo GCP_BUCKET_NAME: $GCP_BUCKET_NAME
echo $GCP_FILE
gcloud storage cp ${GCP_FILE} gs://${GCP_BUCKET_NAME}/backups/${GCP_FILE}

################
# RESTORE BACKUP
#
gcloud sql import sql ${GCP_INSTANCE} gs://${GCP_BUCKET}/backups/${GCP_FILE} \
--database=${GCP_DB_NAME}

```

##################################################################################
##################################################################################

# DOWNLOAD ALL IMAGES
echo GCP_MEDIA_DIR: ${GCP_MEDIA_DIR}
echo " "
gsutil cp -r ${GCP_MEDIA_DIR} .

# UPLOAD ALL IMAGES
cd <BACKUP DIR>
cd images


echo GCP_LOCAL_ICONS: $GCP_LOCAL_ICONS
echo GCP_LOCAL_INAGE: $GCP_LOCAL_INAGE

echo GCP_IMAGE_DIR: $GCP_IMAGE_DIR
echo GCP_ICON_DIR: GCP_ICON_DIR

echo GCP_MEDIA_DIR: ${GCP_MEDIA_DIR}
echo GCP_LOCAL_DIR: ${GCP_LOCAL_DIR}

echo ' '

cd /mnt/c/Users/heidless/Downloads

gsutil -m cp -r \
  "gs://heidless-pfolio-3-bucket/icons" \
  "gs://heidless-pfolio-3-bucket/images" \
  .



gsutil cp -r ${GCP_LOCAL_ICONS} ${GCP_ICON_DIR}




cd ..

cd icons
echo ${GCP_ICON_DIR}
gsutil cp -r * ${GCP_ICON_DIR}
cd ..



#########################################
### IMAGE/FILE Backup



