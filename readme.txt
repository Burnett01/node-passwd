This is a node module for controlling [passwd(5)](http://linux.die.net/man/5/passwd) (/etc/passwd) and [group(5)](http://linux.die.net/man/5/group) (/etc/group) in your nodeJS application.

It was orginally written by Peteris Krumins (@pkrumins) (https://github.com/pkrumins/node-passwd)

Modified by @Burnett01 - now with [group(5)](http://linux.die.net/man/5/group)

------------------------------------------------------------------------------
####Users

```javascript
  var manager = require('passwd-groups');

  //Users

  // add a new user
  manager.addUser('pkrumins', 'password', { createHome : true }, function (status) {
      if (status == 0) {
          console.log('great success! pkrumins added!');
      }
      else {
          console.log('not so great success! pkrumins not added! useradd command returned: ' + status);
      }
  });


  // calls `userdel pkrumins`
  manager.delUser('pkrumins', { sudo : true }, function (status) { ... });

  // locks user pkrumins via `usermod -L pkrumins`
  manager.lockUser('pkrumins', function (status) { ... })

  // unlocks user pkrumins via `usermod -U pkrumins`
  manager.unlockUser('pkrumins', function (status) { ... })

  // gets 'pkrumins' user entry from /etc/passwd
  manager.getUser('pkrumins', function (user) { ... })

  // gets all users from /etc/passwd
  manager.getAllUsers(function (users) {
      users.forEach(function (user) {
          console.log(user.username);
      });
  });
```

A user-entry looks like:

```javascript
{
  username : string,
  password : string(not the real password, just xxxx),
  userId : integer,
  groupId : integer,
  name : string,
  homedir : string,
  shell : string
}
```

####Groups
  
```javascript
  // add a new group
  manager.addGroup('pkrumins', { createHome : true }, function (status) {
      if (status == 0) {
          console.log('great success! group pkrumins was added!');
      }
      else {
          console.log('not so great success! group pkrumins not added! groupadd command returned: ' + status);
      }
  });

  // delete a group
  manager.delGroup('pkrumins', { sudo : true }, function (status) { ... });

  // gets 'pkrumins' group entry from /etc/group
  manager.getGroup('pkrumins', function (group) { ... })

  // gets all groups from /etc/group
  manager.getAllGroups(function (groups) {
      groups.forEach(function (group) {
          console.log(group.name);
      });
  });
  
```

A group-entry looks like:

```javascript
{
  name : string,
  password : string(not the real password, just xxxx),
  id : integer,
  members : array
}
```

##API

```javascript

/*  ++++++++++++++++++++++
    ++++ User Methods ++++
    ++++++++++++++++++++++
*/

exports.addUser = function (username, pass, opts, cb);

exports.delUser = function (username, opts, cb);

exports.lockUser = function (username, opts, cb);

exports.unlockUser = function (username, opts, cb);

exports.passwd = function (username, pass, opts, cb);

exports.getAllUsers = _getUsers;

exports.getUser = function (username, cb);


/*  +++++++++++++++++++++++
    ++++ Group Methods ++++
    +++++++++++++++++++++++
*/

exports.addGroup = function (name, opts, cb);

exports.delGroup = function (name, opts, cb);

exports.getAllGroups = _getGroups;

exports.getGroup = function (name, cb);

```

------------------------------------------------------------------------------

If you need help just file a new issue. Pull-requests are very welcome.

