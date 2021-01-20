# AppleScript

```
--
-- HELPERS
--
-- Check the position of an item 
-- in an array.
on listPositionChecker(theItem, theList)
  repeat with i from 1 to the count of theList
    if item i of theList is theItem then return i
  end repeat
  return 0
end listPositionChecker

-- Check if a number has a leading zero,
-- add it if not.
on leadingZeroChecker(checkNumber)
  if the length of (checkNumber as string) is 1 then return ("0" & checkNumber)
  return checkNumber
end leadingZeroChecker

-- Convert date object to unix timestamp
set unixTimeStamp to my unixDate(current date)

on unixDate(datetime)
	set command to "date -j -f '%A, %B %e, %Y at %I:%M:%S %p' '" & datetime & "'"
	set command to command & " +%s"
	
	set theUnixDate to do shell script command
	return theUnixDate
end unixDate
```