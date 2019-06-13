dockerImgStore
==============

By default docker uses loopback mounted "devices" to store docker images and
metadata. This default storage configuration (100 GB for image storage) leads
to a rather lengthy start up phase of docker when initially launched.

When docker is enabled by default, such as in the Amazon Container Service
images for SUSE Linux Enterprise the slow start up time of docker upon
instance creation provides a sub optimal user experience. Additionally other
services that depend on docker being operational may time out.

The script and systemd unit files in this project address the problem described
above. The script creates a 100 GB device file that is then formatted with
btrfs by default or xfs. The mounted device allows docker to use the btrfs
storage driver or for newer versions of docker overlayfs. This improves the
the startup speed.
