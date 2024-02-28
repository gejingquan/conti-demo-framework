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
docker build -t your_dockername .
cd ..
```


3. Download the conti demo framework and change the docker name to your_dockername

```
git clone https://github.com/zyw-200/conti_afl_framework-master-master    //Replace this url address with the latest framework address
vi conti_afl_framework-master-master/mysite/fuzzing_service/fuzzers/AFLFuzzer/AFLFuzzer.py   //Modify lines 597, 648 and 685 of AFLFuzzer.py and replace them with your_dockername   

```

4. Setup the web server

```
cd conti_afl_framework-master-master
/usr/bin/python3 -m venv conti_afl_framework
source conti_afl_framework/bin/activate
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

 
