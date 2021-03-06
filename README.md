# Assignment  
Language Used: C#  

Test Coverage:  
Functional Testing  

Load Testing  

UI Testing 
# Test Cases
 
#### Test Case 1  : Validate command line should return a job identifier immediately.    
Status: Fail    
Scenarion:curl -X POST -H "application/json -d{"\password\":"\angrymon\"}"http://127.0.0.1:8088/hash                                                                                                
Result: Application waited 5 second to return the Job identifier    


                                                                                     
#### Test Case 2  :  Validate GET accepts job identifier present on the application                            
Status :  Pass    
Scenario Tested : Added existing job ID on curl -H "application/json" http://127.0.0.1:8088/hash/1    
  Result: Verified GET accepted the job ID and gave a result  
 
Secnario Tested : Added non existing job ID on curl -H "application/json" http://127.0.0.1:8088/hash/50b.    
Result: Verified GET did not accept the '50b' job ID and prompted a error "Hash not found".
                                 

#### Test Case 3 :  Validate the correct base64 encoded password for sha-512  password hash displays    
Status : Fail  
Result: Applcation did not return correct base64 encoded password for corresponding SHA-512 hash.
Password: angrymon
##### SHA-512  for angrymon: 02042e87833566bf5ff6300256e601dccafcc22f9de3fdadc960824b47f068639990e790a5e1e4c28c19bc94fb2647201f5a0f6ce0863ee5e3e5272fce62d7e5  
##### Expected Result Base64  for SHA- 512: MDIwNDJlODc4MzM1NjZiZjVmZjYzMDAyNTZlNjAxZGNjYWZjYzIyZjlkZTNmZGFkYzk2MDgyNGI0N2YwNjg2Mzk5OTBlNzkwYTVlMWU0YzI4YzE5YmM5NGZiMjY0NzIwMWY1YTBmNmNlMDg2M2VlNWUzZTUyNzJmY2U2MmQ3ZTU=
##### Actual Result: AgQuh4M1Zr9f9jACVuYB3Mr8wi+d4/2tyWCCS0fwaGOZkOeQpeHkwowZvJT7JkcgH1oPbOCGPuXj5ScvzmLX5Q==


             
#### Test Case 4 - > Validate stat data should display on JSON format  
Status:  Pass  
Scenario Tested: Ran curl http://127.0.0.1:8088/stats.        
Result:  Verified stat data displayed on following JSON format {"TotalRequests":2,"AverageTime":}



#### Test Cases 5 : Validate application return correct JSON total hash request  
Status : Pass

Scenario Tested:  Ran url -X POST -H "application/json -d{"\password\":"\angrymon\"}"http://127.0.0.1:8088/hash two times got the job ID as  1 and 2. Ran curl http://127.0.0.1:8088/stats 
   
Result: The application gave correct total hash request since the server started.The result displayed as follow {"TotalRequests":2,"AverageTime":}  

Scenario Tested: Closed the application and ran curl -X POST -H "application/json -d{"\password\":"\angrymon\"}"http://127.0.0.1:8088/hash one time got the job ID as 1.    
Again ran  curl http://127.0.0.1:8088/stats.

Result: Verified result displayed as follow {"TotalRequests":1,"AverageTime":}    

#### Test Case 6 : Validate application returns correct the average time of a hash request in milliseconds in JSON.    
Status : Fail    
   
Scenario Tested:  Opened exe file.      
Ran curl -X POST -H "application/json -d{"\password\":"\angrymon\"}"http://127.0.0.1:8088/hash    
Again ran curl http://127.0.0.1:8088/stats
 
Result: The system displayed wrong average time as 0 or 447100, the average time should  be around 54400.



#### Test Cases 7 :  Validate software run multiple connection    
Status: Passed    
   
Scenario Tested: Ran multiple command on applcation window.  
 
Result : Verified all of the request returned  the result.


#### Test Case 8 :  Validate when application shutdown, system prompt 200 Empty Response message    
Status : Fail  

Scenario Tested : Ran curl -X POST -d 'shutdown' http://127.0.0.1:8088/hash

Result: no response message displayed on the console window.    


#### Test Case 9 : When one application shuts down, validate any pending request successfully completes.  
Stauts : Pass  
   
Scenario Tested :  Opened a  2 command console.  
On one window,    added a POST to /hash to accept password    
On second window, added shutdown command    
   
Result :  When a both application ran together, post to hash returned the job identifier (first) and then command console closed.    
   

#### Test Case 10: Validate when user closes the application, software does not accept additional password request
Status: Pass
 
Scenario Tested:  Ran curl -X POST -d 'shutdown' http://127.0.0.1:8088/hash and entered curl -H "application/json" http://127.0.0.1:8088/stats on console window.    
   
Result: Verfied curl(n) Failed to connect to port 8088 displayed on the page and did not process the request.  


## Testing multiple connection  


```Apache JMeter
To test multiple connection simultaneously (load testing) we can use Apache Jmeter
1. Create a Thread Group
1.1 - > Create a Number of Threads (number of user request Jmeter will try to simulate)
1.2 - > Ramp-Up Period (in seconds)
1.3 - > Loop Count ( the number of times we want to execute the test)

2.  Add an HTTP Request Defaults
3.  Add an HTTP Request Sampler
4.  Add a View Result in Table Listener
5. Run the Test
```

## Testing adding data
```C#
This is for UI part for entering password

public page AddPassword(string password)
       {
           
           var password  = Driver.FindElement(By.XPath("//input[@id='pasword']"));
           password.SendKeys("angrymon");
           return this;
       }


public page ClickSubmit()
       {
           
           IWebElement item = Driver.FindElement(By.XPath("locator"));
            item.Click();
       }
       
  


```
