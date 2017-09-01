# -Rapyuta-installation-in-Ubuntu14.04-LTS-Trusty-
This gzip folder is a tested version which can install rapyuta in ubuntu14.04(trusty) and run Test demo successfully.
The version of rapyuta is only different from official version in rce/setup/provision file.

Prepare
sudo apt-get install vim

Install indigo ROS
sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
sudo apt-get update
sudo apt-get install ros-indigo-ros-base
sudo rosdep init
rosdep update
echo "source /opt/ros/indigo/setup.bash" >> ~/.bashrc
source ~/.bashrc
sudo apt-get install python-rosinstall

Install rapyuta
sudo apt-get install python-setuptools python-dev git-core
sudo git clone -b master https://github.com/cnsdytzy/-Rapyuta-installation-in-Ubuntu14.04-LTS-Trusty-.git rce
--（del）sudo git clone -b master https://github.com/rapyuta/rce.git rce

cd ~/rce/rapyuta/python-iptables
sudo python setup.py build
sudo python setup.py install

cd ~/rce
sudo chmod 777 ~/rce/install.sh
sudo ./install.sh

--(del)sudo mv ~/rce/setup/provision ~/rce/setup/provision.backup
--(del)sudo cp ~/rce1404/rapyuta/rce/setup/provision ~/rce/setup/provision

sudo chmod 777 ~/rce/rapyuta/rce/setup/provision
sudo ./setup/provision all

export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:/home/rapyuta/rce/rapyuta/rce/test
echo 'export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:/home/rapyuta/rce/rapyuta/rce/test' >> ~/.bashrc
. ~/.bashrc


If Success Then Test:
sudo vim ~/.rce/config.ini
[machine/packages]
Test=/home/rapyuta/rce/rapyuta/rce/test 

sudo rce-make
rosmake Test
exit
cd ~/rce/rapyuta/rce/test/nodes
sudo chmod 777 *

Addition Error1:
$ sudo rm /var/crash/*
$ sudo vim /etc/default/apport
enabled=0
$ sudo restart apport

Addition Error2:
if display "SyntaxWarning: The publisher should be created with an explicit keyword argument 'queue_size'."
then modify "self.publisher = rospy.Publisher(self.topic, self.message)" to "self.publisher = rospy.Publisher(self.topic, self.message, queue_size=10)".




