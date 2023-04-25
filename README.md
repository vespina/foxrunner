# foxrunner
TCP/IP Server to allow VFP code remote execution


## OBJECTIVE
The idea is to allow any app to run arbitrary VFP code on a remote server and then query the result of the execution, using a REST-like interface.

## HOW IT WILL WORK

* Foxrunner will be installed in a computer inside a LAN
* Other computers in the network will send a request to foxrunner service to execute arbitrary code
* Computers will send a different request to foxrunner to query the execution state of a running job


## JOB INFO
Foxrunner will accept a REST-like request to start a job, and the request will contain a JSON string
containing all the required information for the job:

    {
      "reference": "Brief description of the job",
      "origin": "name of the computer that originates the request",
      "user": "name of the user that owns the request",
      "code": "code to run, base64-encoded",
      "when": "date-time when the process should be run (optional)",
      "priority": (value between 0 and 10 that indicates the priority of the job),
      "parameters": [ { "name": "parameter name", "value": (parameter value) ] ...]
    }
    
Foxrunner wil reply with an object containing information about the job accepted:

    {
        "id": "job unique id",
        "received": "Date/time when the job was received",
        "position": "Position of the job inside the execution queue"
    }
   
When asked about the status of a running job, foxrunner will answer with the following object:

    {
       "id'; "job unique id",
       "status": "queued | running | completed | failed",
       "errormsg": "Description of any error ocurred during job execution",
       "started": "date/time when job was started",
       "completed": "date/time when job was completed",
       "duration": (job duration in seg)
    }
    
   
    
