To open jupyter from any remote client.
--------------------------------------
from remote 
lsof -ti:5901 | xargs kill -9
