<template>
		<div>
			<div class="form">
				<div class="field">
					<label>Фамилия</label>
					<input type="text" v-model="elem.surname">
				</div>
	
					<div class="field">
						<label>Имя</label>
						<input type="text" v-model="elem.name">
					</div>
	
					<div class="field">
						<label>Отчество</label>
						<input type="text" v-model="elem.otch">	
					</div>
							
					<div class="field">
						<label>Телефон</label>
						<input type="text" v-model="elem.phone">
					</div>
						
			
						<p class="check"><input type="checkbox" v-model="elem.best">Избранное</p>
							
						<button class="btn btn-outline-primary" v-on:click="Add()">Добавить</button>
						
							
						<div class="radio">
							<div class="form-check form-check-inline">
								<input class="form-check-input" value="surname" type="radio" v-model="sort" @click="Sort('surname')"><p class="form-check-label">Сортировать по фамилии</p>
							</div>
					
							<div class="form-check form-check-inline">
								<input class="form-check-input" value="name" type="radio" v-model="sort"  @click="Sort('name')"><p class="form-check-label">Сортировать по имени</p>
							</div>
						</div>
			</div>
		
		
			<div class="note">
				<div class="note-in">
					<ul>
						<li class="field" v-for="(item,id) in bests" v-bind:key=id>
								<label>{{item.surname}} {{item.name}} {{item.otch}} {{item.phone}}</label>
								<div class="features">
									<span>★</span>
									<img src="../assets/buck.png" class="delete" href="#" @click="Delete('best',id)" onmouseover="this.src='../assets/buck_hover.png'" onmouseout="this.src='../assets/buck.png'">
								</div>
								
						</li>
		
							<li class="field" v-for="(item,id) in contacts" v-bind:key=id>
								<label>{{item.surname}} {{item.name}} {{item.otch}} {{item.phone}} </label>
								<div class="features">
									<img src="../assets/buck.png" class="delete" href="#" @click="Delete('contact',id)" onmouseover="this.src='../assets/buck_hover.png'" onmouseout="this.src='../assets/buck.png'">
								</div>
								
							</li>
						</ul>
					</div>
					
			</div>
		</div>
</template>

<script>
	export default{
		data(){
			return{
				elem:{
				surname:"",
				name:"",
				otch:"",
				phone:"",
				best:false
				},
				sort:"surname",
				contacts:[],
				bests:[]
			}
			
		},
		methods:{
			async Add(){
				
				if(!(this.elem.surname==""||this.elem.name==""||this.elem.otch==""||this.elem.phone=="")){
					if((this.contacts.find(x => x.phone === this.elem.phone)===undefined)&&(this.bests.find(x => x.phone === this.elem.phone)===undefined)){
						if(!this.elem.best){
							this.contacts.push({
						  		surname:this.elem.surname,
								name:this.elem.name,
								otch:this.elem.otch,
								phone:this.elem.phone,
								best:this.elem.best
							});
						}

						else{
							this.bests.push({
								surname:this.elem.surname,
								name:this.elem.name,
								otch:this.elem.otch,
								phone:this.elem.phone,
								best:this.elem.best
							});
						}

						try{
							await this.$http
							.post("http://localhost:3000/notes",this.elem);
							this.Update();
						}

						catch(err){
							console.error(err);
						}
						this.elem.surname="";
						this.elem.name="";
						this.elem.otch="";
						this.elem.phone="";
						this.elem.best="";

						if(this.sort==="surname"){
							this.contacts.sort((a, b) => a.surname > b.surname ? 1 : -1);
							this.bests.sort((a, b) => a.surname > b.surname ? 1 : -1);
						}

						if(this.sort==="name"){
							this.contacts.sort((a, b) => a.name > b.name ? 1 : -1);
							this.bests.sort((a, b) => a.name > b.name ? 1 : -1);
						}
					}
					
					else{
						alert("Такой номер уже существует!");
					}
				}
				
				else{
					alert("Поля не должны быть пустыми!");
				}
			},
		async Update(){
			try{
				let res=await this.$http.get("http://localhost:3000/notes");
				this.notes=await res.json();

			}

			catch(err){
				console.error(err);
			}
		},

		Sort:function(param){
			if(param=="surname"){
				this.contacts.sort((a, b) => a.surname > b.surname ? 1 : -1);
				this.bests.sort((a, b) => a.surname > b.surname ? 1 : -1);
			}
			else if(param=="name"){
				this.contacts.sort((a, b) => a.name > b.name ? 1 : -1);
				this.bests.sort((a, b) => a.name > b.name ? 1 : -1);
			}
			
		},

		Delete: function(item,id){
			if(item=='best')this.bests.splice(id, 1);
			else if (item=='contact')this.contacts.splice(id, 1);
			
		}
		},
		created(){
			this.Update();
		}  
	}
</script>