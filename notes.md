### To open jupyter from any remote client.
-------
The remote server can be any \*nix system (AWS EC2, Linux, Unix)

**On remote**

* Install Jupyter using `conda` or `pip` 

* If you have installed Jupyter inside a virtual environment then
	* run the following on the command line of the remote server
	`source activate <myenv>`
	`conda install ipykernel`
	`python -m ipykernel install --user --name <myenv> --display-name "Python <(myenv)>"`

	The above will ensure that the notebook you eventually launch will have the option to use Python version installed inside the environment, under the "Change Kernel" option.

* Run the following command

`jupyter notebook --no-browser --port=8889`

Choose a port number you prefer.

* Leave this window as is. Note that there is a token given by Jupyter, which might have to be entered into the local browser that will be used to launch Jupyter

**On th local system**
(This is for mac OS)

* Run the following 

`ssh -N -f -L localhost:8888:localhost:8889 h<Username>@<remote server>`

Sometimes the above gives error, such as

`channel 2: open failed: connect failed: Connection refused`

This error can be debuged using the same command in a verbose manner

`ssh -N -f -L localhost:8888:localhost:8889 <Username>@<remote server> -v -v -v`

You can use upto three `-v` to increase verbosity

In my case the listener or the local had an IPv6 Ip address.

I solved it by running the following command

`ssh -f hvakade@sjc-ads-1110 -L [::1]:8888:127.0.0.1:8889 -N`

Note 127.0.0.1 points to the `localhost`

* Now you can open the jupyter notebook by going to your browser on the local machine and typing "http://localhost:8888". Youn can also change kernel to point to the Python installed in virtual environment.

* Because I was running to errors everytime I had to kill the Application running on the port 8888. You can do so by running the following command,

`lsof -ti:8888 | xargs kill -9`
