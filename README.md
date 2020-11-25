
# Distributed File System using Python
## Project Description
A Distributed File System is a cluster of servers hosting potentially large files that needs to be stored in a secure and reliable manner.This project is currently limited to distributing text files only.

Written in Python with a server-client architecture, A given file is distributed (using the PUT method) from the Client to the Servers in various chunks, which can be retrieved (using the GET method) and used to reconstruct the file. 

The built-in redundancy in the way the file chunks are stored in the four servers ensures that if a given server fails, the file can still be reconstructed. Traffic optimization is achieved by not sending any redundant file chunks unless necessary. Some security is implemented via authentication, and storage of password hashes. 

### File Chunk Pair Locations

|hash mod|DFS1|DFS2|DFS3|DFS4|
|:--:|:-----:|:-----:|:-----:|:-----:|
| 0  | (1,2) | (2,3) | (3,4) | (4,1) | 
| 1  | (4,1) | (1,2) | (2,3) | (3,4) |
| 2  | (3,4) | (4,1) | (1,2) | (2,3) |
| 3  | (2,3) | (3,4) | (4,1) | (1,2) |

## Dependencies
rpyc for RPCs in Python

## Running the Project 
**RUN** (any number of) servers first, then the client:
Open multiple terminals for this to work.
Terminal 1:
```
$ py dfs1.py
```

Terminal 2:
```
$ py dfs2.py
```

Terminal 3:
```
$ py dfs3.py
```

Terminal 4:
```
$ py dfs4.py
```

Terminal 5:
```
$ py client.py
```
	
_Authenticate with these details:_

```	
AnujS: Bluepanda
AnujK: wiger
```
	
md5 is used for hashing the passwords.

## Commands
**`[PUT]` method**:

`PUT` sends any text files located in the source folder into the numbered server folders for distributed storage.
	
`PUT` splits files into "n" chunks ("n" being the number of servers, here, it is 4), stores pairs of chunks into each server after hashing file and taking the modulus of the hash to ensure fair distribution, according to the table below. The duplication of files ensures reliability if 1 server is down.


 **`[GET]` method**:

`GET` retrieves files from the servers into a user folder within the directory. 
	
`GET` joins the 4 chunks into a single file. If a single server is down, this operation can still succeed. If the operation fails, the file is not created and the user gets a 'Transfer failed' message.


**`[LIST]` method**:

`LIST` provides a list of file chunks a user has stored in the server. From the list, a user can glean file names and specify a file to `GET`. If a user chooses `PUT` within `LIST`, the user can determine a file to send for distributed storage.


## To Do 
- Using an external NoSQL database for User Authentication 
- Dealing with text artifacts
- DELETE function
- Encrypting all traffic

--- 