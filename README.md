# P100-helpfile
Keep the Pisces P100 working (3 ways)

DONT FOLLOW ALL THE STEPS, you have to choose wich option you will use.
Please read the instructions first, than decide what option you are going to use.

==========

Using crankk docker only:
sudo docker run --privileged --restart always -v /:/host --net=host --pid=host --name crankk -v crankk_data:/data -itd crankkster/crankk:latest
