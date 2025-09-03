# conti-demo-framework
This project introduces how to install the full version of conti demo framework.

1. Install the root cause analysis module

```
mkdir conti-demo-framework
cd conti-demo-framework
git clone https://github.com/gejingquan/RCA_v1
cd RCA_v1
./RCA_conti_demo_installation.sh
cd ..
```

2. Create docker

```
git clone https://github.com/gejingquan/conti-demo-docker
cd conti-demo-docker
```

If you want to fuzz test software for Ubuntu 20.04, build the RCA-brach Docker image.

```
git checkout RCA-branch
docker build -t your_dockername1 .
```

If you want to fuzz test software for Ubuntu 22.04, build the main branch Docker image.

```
git checkout main
docker build -t your_dockername1 .
```

Then, build the AutoPatcher docker image
```
cd ..
git clone https://github.com/MarkLee131/AutoPatcher
cd AutoPatcher
docker build -t your_dockername2 .
cd ..
```


3. Download the conti demo framework and change the docker name to your_dockername

```
git clone https://github.com/zyw-200/conti_afl_framework-master-master    // Replace this url address with the latest framework address
vi conti_afl_framework-master-master/mysite/fuzzing_service/fuzzers/AFLFuzzer/AFLFuzzer.py   // Modify lines 599, 650 and 710 with your_dockername1, modify line 685 with your_dockername2.    

```

4. Setup the web server

```
cd conti_afl_framework-master-master
/usr/bin/python3 -m venv conti_afl_framework
source conti_afl_framework/bin/activate
pip install -r mysite/requirements.txt
cd mysite
mkdir media
python manage.py makemigrations fuzzing_service
python manage.py migrate
python manage.py flush
python manage.py createsuperuser 
fp 
fp@gmail.com 
fp123
python manage.py runserver *.*.*.*:8040
```

5. Before running RCA, disable ASLR in advance.
Open a new terminal and run the following command:
```
su
echo 0 | sudo tee /proc/sys/kernel/randomize_va_space
```


 
