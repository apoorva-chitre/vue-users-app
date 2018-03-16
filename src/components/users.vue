<template>
    <div class="users">
		<h1>Users</h1>
		<h3>Add a new user</h3>
		<form v-on:submit="addUser">

			<input type="text" v-model="newUser.name" placeholder="Enter Name">
			<br>
			<input type="text" v-model="newUser.email" placeholder="Enter Email">
			<br>
			<input type="submit" value="Add user">

		</form>
		<br>
		<h3>List of active users</h3>
			<table width="75%">
				<tr>  
				    <th>Name</th>
				    <th>Contacted</th>
				    <th>Verified</th>
				    <th> Delete </th>
				</tr>

				<tr v-for="user in users">  
					<td>
						<span :class="{contacted: user.contacted}">
							<span :class="{verified: user.verified}">
								{{ user.name}} : {{ user.email }} 
							</span>
						</span>
					</td>

				    <td><input type="checkbox" class="toggle" v-model="user.contacted"></td>
				    <td><input type="checkbox" class="toggle" v-model="user.verified"></td>
				    <td><button v-on:click="deleteUser(user)">x</button></td>
				    
				</tr>  
			</table>	

    </div> 
</template>


<script>
	export default {
		name: 'users',

		data() {

			return {

				newUser: {},
				users: [

				]
				
			}
		}, 

		methods: {

					addUser: function (e) {

						this.users.push( {

							name: this.newUser.name,
							email: this.newUser.email,
							verfied: false,
							contacted: false
						});

						e.preventDefault();
					},

					deleteUser : function(user) {

						this.users.splice(this.users.indexOf(user), 1);

					}

					
				},

				created: function() {
					this.$http.get('https://jsonplaceholder.typicode.com/users')
					.then(function(response) {
						this.users = response.data;
					});

				}
			}
	
</script>


<style scoped>


.users {

	margin: 0 auto;
	width:100%;
}

table {

	border: 2px solid #eee;
	
}

.contacted {

	text-decoration: line-through;
}
.verified {

	color: red;
}
	#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>