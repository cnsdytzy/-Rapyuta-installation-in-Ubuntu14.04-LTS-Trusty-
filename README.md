# -Rapyuta-installation-in-Ubuntu14.04-LTS-Trusty-
This gzip folder is a tested version which can install rapyuta in ubuntu14.04(trusty) and run Test demo successfully.
The version of rapyuta is only different from official version in rce/setup/provision file.


2017/09/02
rce/client/interface.py line 485
modify "iself._pub = rospy.Publisher(self._addr,self._conn.loader.loadMsg(*self._args))"
to  "iself._pub = rospy.Publisher(self._addr,self._conn.loader.loadMsg(*self._args),queue_size=10)".




