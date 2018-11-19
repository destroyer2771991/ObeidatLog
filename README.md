# ObeidatLog
C#.Net very fast text, XML files, or SQL database log for web applications.
I needed to record every request in my web application and after 3 months of searching and practicing for the best way to log a record without affecting the time of web request and performance.

### The main idea in this log is the sacrifice:
1. **Instantaneous:** What I mean is that this log does not write the request instantaneously; it may be delayed for a maximum of 30 seconds, so as to ease the pressure on the IO.
2. **Ordering:** This is because the requests written in the log are written with the time and thus there is no need to arrange which expedits the writing of the requests once.

### Its advantages are as follows:
- It can carry a very large number of concarent requests; by stored list of requests in a series with a capacity an item and write it once upon completion of the arrival to the limit or after 30 seconds.
- Replace the IO lock with the [Blocking Collection](https://docs.microsoft.com/en-us/dotnet/api/system.collections.concurrent.blockingcollection-1?view=netframework-4.7.2), which ensures the speed and it is [thread-safe](https://msdn.microsoft.com/en-us/library/a8544e2s.aspx).
- All actions in the log run on different thread and therefore do not affect the speed or performance of the system.
- Record 3 different types:
  - text file.
  - XML file.
  - Database tabels.
- Replace the check-conditions when choosing the level or type by template design pattern so reduce the time of check the level or type in every write log item.
- When selecting a file (text or XML), the log creates a file for each day and names it with system name and the date of the day for each level of the record. When selecting a database, the log creates a table for each level (if not exists) with system name and the level.
- The record contains 4 different levels:
  - None.
  - Exceptions only.
  - Exceptions and Information.
  - Exceptions, Information and debug.
- The log automatically excludes base64 and any properties added in configuration.
- In exception the log write with the exception message:
  - File name. 
  - Method name.
  - Line number.
  - Caption (optional).
- The exception message come from every inner-exceptions(if exests) for this exception.
- The debug wite with every request body:
  - IP address.
  - Device name. 
  - HTTP method.
  - Username, 
  - Client name.
  - Url for this request.
