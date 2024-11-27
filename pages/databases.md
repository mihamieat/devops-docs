# mongodb
- after install, start the mongod service
```sh
sudo systemctl start mongod
```
- command to access shell
```sh
mongosh
```
- connect to admin user
```javascript
use admin
```
- create a root user
```javascript
admin > db.createUser({user: "root", pwd: "password", roles: ["root"]})
```
- change ***/etc/mongod.conf*** to enable authorization
file location on macos might be in /opt/homebrew/etc/.
it is preferable to create a conf file that overrides the original and try not to edit the original conf file. (e.g. ```
/opt/homebrew/etc/mongo.d/security.conf
```)
```sh
security:
	authorization: "enabled"
```
- restart mongod service
```sh
sudo systemctl restart mongod
brew services restart mongodb-community # on macos
```
- connect with the new added user
```sh
mongosh -u root -p
```
- (create and) connect to a document
```javascript
use my_document
```
- insert data to a collection
```javascript
db.collection('post').insertOne({
	"title": "mon premier article",
	"content": "mon contenu..."
})
```
- command to find data
```sh
my_document > db.find()
```
- mongodb connection string
```sh
mongodb://<credentials>@127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.3.3
```
## mongosh useful commands
```sh
show dbs
use tickethack
mongoimport -u mihamieat -p password --authenticationDatabase admin --db tickethack --collection trips --file ~/Downloads/trips.json --jsonArray
show collections
db.trips.find().pretty()
```
