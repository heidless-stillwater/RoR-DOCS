
## [Cloud SQL(MySQL, PostgreSQL and Microsoft SQL Server) automatically backup and stores into the GCS bucket](https://medium.com/google-cloud/cloud-sql-mysql-postgresql-and-microsoft-sql-server-automatically-backup-and-stores-into-the-gcs-d01cf3677c67)


PROJECT:    heidless-pfolio-1
INSTANCE:   heidless-pfolio-1-backend-0-instance-0
DB:         heidless-pfolio-1-backend-0-db-0	
DB_USER:    heidless-pfolio-1-backend-0-user-0	


```
gcloud iam service-accounts list
--
449207231494-compute@developer.gserviceaccount.com
--

##########################
# ERROR: (gcloud.sql.export.sql) HTTPError 403: The service account does not have the required permissions for the bucket.
--
FIX: Export instance via Console to add permission. Then CLI works fine

GOOGLE Console->SQL-><INSTANCE>->Export

--
##########################
```

# Ruby Apps
```
gcloud init
--
heidless-ror-0
heidlessemail05@gmail.com
heidless-ror-0
europe-west2-a
--
```
## alpha-blog
```
export BK_PROJECT=heidless-ror-0
export BK_INSTANCE=alpha-blog-0-instance-0
export BK_DB=alpha-blog-0-db-0		
export BK_USER=alpha-blog-0-user-0	
export BK_BUCKET=gs://heidless-ror-0-alpha-blog-0-bucket-0
export BK_COMMENT='LatestSnapshot'
export BK_FILE=${BK_INSTANCE}-${BK_COMMENT}-${BK_TIMESTAMP}.gz
export BK_TIMESTAMP=`date +%s`

echo $BK_TIMESTAMP

gcloud sql export sql ${BK_INSTANCE} ${BK_BUCKET}/backups/${BK_FILE} \
--database=${BK_DB} \
--offload

# download backup
gcloud storage cp ${BK_BUCKET}/backups/${BK_FILE} .


gcloud storage cp gs://heidless-pfolio-0-bucket/images/* .


# upload backup

gcloud storage cp ${BK_FILE} ${BK_BUCKET}/backups/${BK_FILE}

####################################
# delete & re-create DB table
##
echo 're-create DB'
echo $BK_DB
echo $BK_INSTANCE
echo ' '
gcloud sql databases delete $BK_DB \
    --instance $BK_INSTANCE

## allow delete to settle - perhaps through Console

gcloud sql databases create $BK_DB \
    --instance $BK_INSTANCE

####################################

# restore (import) DB
gcloud sql import sql ${BK_INSTANCE} ${BK_BUCKET}/backups/${BK_FILE} \
--database=${BK_DB} \

```
########################################################################
####### Heidless pfolio

```
gcloud init
--
heidless-pfolio-1
heidlessemail05@gmail.com
heidless-pfolio-1-backend-0-instance-0
europe-west2-a
heidless-pfolio-1-bucket

--
```
## TAKE BACKUP
```
--
# set permissoons on INSTANCE service account
export SQL_SVC_ACC=`gcloud sql instances describe ${BK_INSTANCE} | grep serviceAccountEmailAddress`
echo $SQL_SVC_ACC
--
serviceAccountEmailAddress: p449207231494-mxctja@gcp-sa-cloud-sql.iam.gserviceaccount.com
--
gsutil iam ch serviceAccount:p449207231494-mxctja@gcp-sa-cloud-sql.iam.gserviceaccount.com:objectAdmin \
gs://heidless-pfolio-1-bucket
--

timestamp=`date +%s`
MSG=2nd-DRAFT

export BK_PROJECT=heidless-pfolio-1
echo PROJECT: $BK_PROJECT

export BK_INSTANCE=$BK_PROJECT-backend-0-instance-0
echo INSTANCE: $BK_INSTANCE

export BK_DB=$BK_PROJECT-backend-0-db-0
echo DB: $BK_DB
		
export BK_USER=$BK_PROJECT-backend-0-user-0
echo USER: $BK_USER

export BK_BUCKET=gs://${BK_PROJECT}-bucket
echo BUCKET: $BK_BUCKET

export BK_COMMENT='LatestSnapshot'
echo COMMENT: $BK_COMMENT

export BK_FILE=${BK_INSTANCE}-${BK_COMMENT}-${BK_TIMESTAMP}.gz
echo FILE: $BK_FILE

export BK_TIMESTAMP=`date +%s`
echo TIMESTAMP: $BK_TIMESTAMP

echo " "

gcloud sql export sql ${BK_INSTANCE} ${BK_BUCKET}/backups/${BK_FILE}    \
--database=${BK_DB}	 \
--offload

```

# DOWNLOAD BACKUP
gcloud storage cp ${BK_BUCKET}/backups/${BK_FILE} .

# RE-CREATE DB
echo 're-create DB'
echo $BK_DB
echo $BK_INSTANCE
echo ' '
gcloud sql databases delete $BK_DB \
    --instance $BK_INSTANCE

gcloud sql databases create $BK_DB \
    --instance $BK_INSTANCE

# UPLOAD BACKUP
FILENAME=heidless-pfolio-1-backend-0-instance-0-LatestSnapshot-1718183102.gz
gcloud storage cp  ${FILENAME} ${BK_BUCKET}/backups/${FILENAME}

# RESTORE BACKUP
FILENAME=heidless-pfolio-1-backend-0-instance-0-LatestSnapshot-1718183102.gz
gcloud sql import sql ${BK_INSTANCE} ${BK_BUCKET}/backups/${FILENAME} \
--database=${BK_DB}

# DOWNLOAD ALL IMAGES
IMAGE_DIR=${BK_BUCKET}/images
echo ${IMAGE_DIR}
gsutil cp -r ${IMAGE_DIR} .

# UPLOAD ALL IMAGES
IMAGE_DIR=${BK_BUCKET}/images
echo ${IMAGE_DIR}
cd ${IMAGE_DIR}
gsutil cp -r * ${IMAGE_DIR}



