---
title: User metadata
keywords: web
sidebar: web_sidebar
toc: true
permalink: web_user.html
folder: web
---


## Product description 

User metadata refer to user information, including nickname, avatar, age, mobile phone number, etc.
User metadata are optional services. users can maintain it by themselves if they do not want to storesensitive information in the Agora server.

Use the user attribute function to obtain the following capabilities:

- Reading and writing ability of standard user metadata, including nickname, avatar url, email address, phone number, gender, signature, birthday;
- Customize the read and write capabilities of user metadata, provide custom extensions, and add multiple metadata through JSON strings.

## Integration overview

The SDK provides user-attribute information hosting services, allowing users to save common fields such as avatars, nicknames, and an extended field.

The user attribute information that can be managed by Agora is as follows:
* nickname - nickname
* avatarurl - avatar url
* mail - email
* phone - phone
* gender - gender
* sign - sign
* birth - birthday
* ext - extension 

## Set user metadata

Each user only has permission to set his own user metadata.
When setting user metadata, you can set all metadata of the user, or only one attribute of the user

- Set multiple user metadata 

```js
let options = {
    nickname: 'nick name',
    avatarurl: 'http://avatarurl',
    mail: '123@gmail.com',
    phone: '16888888888',
    gender: 'female',
    birth: '2000-01-01',
    sign: 'a sign',
    ext: JSON.stringify({
            nationality: 'China',
            merit: 'Hello，world！'
        })
}
WebIM.conn.updateOwnUserInfo(options).then((res) => {
    console.log(res)
})
```
-   Set individual user metadata

```js
WebIM.conn.updateOwnUserInfo('nickname', 'Tom').then((res) => {
    console.log(res)
})
```
## Get user metadata

When getting user metadata, you can get all the metadata of the user, or you can get the metadata specified by the user, such as getting only nickname, avatar, etc.

-Get all metadata of the user

The interface for obtaining all metadata of a user is as follows:

```js
/**
 * @param {String|Array} users - user id
 */
let users = 'user1' || ['user1', 'user2']
WebIM.conn.fetchUserInfoById(users).then((res) => {
    console.log(res)
})
```
-   Get a single attribute of the user

The interface for obtaining a single attribute of a user is as follows:
```js
/**
 * @param {String|Array} users - user id
 * @param {String|Array} properties - query metadata
 */
WebIM.conn.fetchUserInfoById('userId', 'nickname').then((res) => {
    console.log(res)
})

// Query multiple user metadata at the same time
WebIM.conn.fetchUserInfoById(['user1', 'user2'], ['nickname', 'avatarurl']).then((res) => {
    console.log(res)
})
```
## User avatar management

Agora User-Attribute Hosting Service is not responsible for managing user avatar files, which only stores the remote url address of avatar files. Users need to use third-party file hosting services such as Alibaba Cloud and Tencent Cloud to store avatar files. When a user sets an avatar, he needs to upload the avatar file to a third-party file hosting server first, and then pass the url address obtained after uploading to the avatar url field of the user attribute to set the user attribute. When displaying the avatar, get the user metadata from the SDK first. Next,Please get the avatar url field, and then display the remote avatar image on the UI layer.

## Card message 

There is no card-type message in the SDK. The sending and receiving of card messages in the Demo use the existing custom message type, by specifying the event of the custom message as \"userCard\", and adding required Agora id, nickname, and avatar in the ext to display the user’s business card. 
