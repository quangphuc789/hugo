+++
title = "Enhancement of data security for JWT"
draft = false
date = "2016-12-31T05:53:03+08:00"

+++

# Enhancement of data security for JSON Web Token (JWT) 

Given the nature of HTTP is stateless, full fetch web application would normally implement a session mechanism that allows the consistency and security of user activities. These information will be stored inside backend database and browser cookies. For a lightweight Rest API server, JWT provides a standard way to communicate between endpoints, everything you need is an encoded string of a few JSON objects. JWT can perform some certain tasks:
 * Encode data in URL friendly format
 * Validate some trivial meta requirements at endpoints
 * Verify the data integrity at endpoints

However, JWT does not ensure:
 * Man in the middle (MITM) attack
 * Data confidentiality

Let's talk about these two.

### 1. Man In The Middle (MITM) Attack

Imagine you are writing a letter to your mom through post. This letter is personal and confidential. Let us assume both you and your mom are very careful, no one else could do anything when the letter is with you two. However, the moment when you posted the mail till its arrival at your mom place, anything can happen. Somebody may secretly read, or even steal it away. You need to write in an secret language that only you and your mom understand. So even if the letter is leaked out, no sensitive information is lost.

For data communication, when you send your data across different machines, someone in the middle of the connection can grab the data and manipulate it. The only way you can solve this problem is to secure the connection. That's why you need to move from HTTP to HTTPS.

HTTPS secures the data confidentiality while it is sent across the connection by using encryption at the sender and decryption at the receiver. However this does not help if you lose control of your data before or after sending.

###  2. Data Confidentiality

JWT ensures data is validated with certain meta requirements (claims), and verified that it is not tampered by anyone else. So data integrity is guaranteed. But even if you use HTTPS, anybody will be able to decode the tokens and make sense of your data.

If you are building government related agency apps, user data is the life blood, e.g: email, name, house address, social IDs, driving license, bank account, etc. You need to make sure no one can make sense of data except the trusted application.

Apply a encryption to your data before encoding into JWT could secure the app in a much better way. Do checkout JWE, or implement a simple encryption mechanism.

