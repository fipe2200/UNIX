# 2024-01-08
![[Pasted image 20250104115503.png]]

---
# 2024-06-05
![[Pasted image 20250104115521.png]]

If we have the default permissions 777, and apply these umasks, we get:

777 - 755 = 22 
777 - 500 = 277 
777 - 110 = 667 
read, write and execute privileges are determined using the octadecimal system.
Users Groups Others
rwx      rwx       rwx 
000      000      000 (or any other combination of one's and zero's) 

Let's start with the resulting permission 22: 
the octadecimal representation of this value is 000 010 010 
This means that the owner will have no rights, the group will only have write privileges, and other users will also only have write privileges

The octadecimal representation of 277 is 010 111 111 
This means that the owner can only write to the file, but can't read or execute it. Both the group and other users can read, write, and execute the file.

The octadecimal representation of 667 is 110 110 111 
This means that the owner and groups have read and write permissions, but no execute permissions. The other users have all permissions; read, write, and execute. 

For 22, the owner will have no rights at all, and not the group nor others will even have read permissions. This makes the resulting permissions of 22 highly impractical. 

For 277, the owner can only write, which is very restrictive. The group has full privileges, but other users also have full privileges, which can be a security hazard since unauthorized users can do whatever they want with the file. 

For 667, the user and groups have read and write permissions, which might be appropriate, but the other users still have all rights which is not a safe thing.

# 2024-08-27
![[Pasted image 20250104115539.png]]
## **ls**
- List files
	  
  #Example 
	Will list all files including hidden files (files with names beginning with a dot)
	`ls -la`
	  
	List  files with info
	`ls -l` 
	 ```
	 drwxr-xr-x   6 eva        users         1024 Jun  8 16:46 sabon
	 -rw-------   1 eva        users         1564 Apr 28 14:35 splus
	 ``` 
	 
## **cd**

## **cat**

## **nano**

## **chmod**

## **chown**
