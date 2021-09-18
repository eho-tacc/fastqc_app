# FastQC Tapis App

## Testing

```bash
docker build -f Dockerfile --force-rm -t enho/fastqc:0.11.9 .
mkdir tests
cd tests
wget https://github.com/sequana/fastqc/raw/master/test/data/data_R1_001.fastq.gz
gzip -d data_R1_001.fastq.gz
cd ..
docker run -v $PWD/tests:/tests enho/fastqc:0.11.9 perl /FastQC/fastqc /tests/data_R1_001.fastq
tapis files upload agave://eho.stampede2.storage/apps/fastqc-0.11.9 tests
tapis jobs submit -F job.json
```