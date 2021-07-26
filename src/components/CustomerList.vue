<template>
    <div class="container">
		<!-- Search bar-->
		<div class="search">
			<div class="search-parent">
				<div class="search-bar" >
					<b-form-input
						@input="search_text()"
						v-model="search.text"
						type="text"
						placeholder="Find customers"
					></b-form-input>
					<span class="search-icon">
					<i class="fa fa-search"></i>
					</span>
				</div>
				<div class="search-sortby">
				<b-form-select @input="sort()" v-model="search.filter" :options="options"/>
				</div>
			</div>
		</div>
        <!-- list customers -->
		<transition name="list" mode="out-in" >
				<div class="columns is-multiline is-mobile" v-if="filteredCustomers.length > 0" >
					<div  class="column is-3-widescreen is-3-desktop is-4-tablet'" v-for="customer in filteredCustomers" :key="customer.id">
						<CustomerCard :customer="customer" :url="common_url"/>
					</div>
				</div>	  
		</transition>
		<!-- Search results message -->
		<div v-if="filteredCustomers.length ==0">
          <div class="columns is-multiline is-mobile">
            <div class="column">
              <h3 class="title is-4 has-text-centered">no customer(s) found with the search criteria</h3>
            </div>
          </div>
          </div>
	</div>
</template>
<script>
import CustomerCard from './CustomerCard.vue'
import axios from 'axios'

export default {
    components: {
        CustomerCard
    },
	mounted () {
         this.fetchCustomers()
	},
	data () {
		return {
			search: { filter: null, text: "" },
			options: [
				{ value: null, text: "Filter by Name" },
				{ value: "ascending", text: "A-Z" },
				{ value: "descending", text: "Z-A" }
			],
			customers_list: [],
			total_customers_list: [],
			common_url: "https://placekitten.com/380/200"
		}
	},
	methods: {
		sort() {
			console.log(this.search.filter);
			this.search.filter == "descending"
				? this.customers_list.sort(function(a, b) {
					let fa = a.name.toLowerCase(), fb = b.name.toLowerCase();
					if (fa > fb) {
						return -1
					}
					if (fa < fb) {
						return 1 
					}
					return 0
				}) :
				this.customers_list.sort(function(a, b) {
					let fa = a.name.toLowerCase(), fb = b.name.toLowerCase();
					if (fa < fb) {
						return -1
					}
					if (fa > fb) {
						return 1 
					}
					return 0
				});
			// console.log(this.customers_list)
       },
       search_text() {
		let inside = this
			console.log('search input :' +this.search.text)
			this.customers_list = this.total_customers_list.filter(function(customer) {
				return (
				customer.name
					.toLowerCase()
					.indexOf(inside.search.text.toLowerCase()) != "-1"
				) 
			});
			// console.log(this.customers_list)
			
       },
	async fetchCustomers () {
			try {
				const url = `http://jsonplaceholder.typicode.com/users`
				const response = await axios.get(url)
				// console.log(response.data)
				this.customers_list = response.data
				this.total_customers_list = response.data
			} catch (err) {
				console.log(err)
			}

       }
	},
	computed : {
		filteredCustomers () {
			return this.customers_list
		}
	}
    
}
</script>
<style scoped lang="scss">
	.search {
		&-parent {
			padding: 10px 20px;
			display: flex;
			flex-flow: row wrap;
			justify-content: space-between;
			align-items: center;
			// background-color: rgb(197, 194, 194);
		}

		&-bar {
			position: relative;
			width: 200px;
			height: 50px;
			left: 1px;
			top: 1px;
			

			input {
				padding-left: 30px;
			}
		}

		&-icon {
			position: absolute;
			top: 8px;
			left: 8px;
		}

		&-sortby {
		display: flex;
			flex-direction: column;
			// justify-content: center;
			// align-items: center;
			padding: 8px 12px 8px 16px;

			position: relative;
			width: 222px;
			height: 50px;
			left: 0px;
			top: 0px;

			/* Action Secondary/Default */

			background: #FFFFFF;
			border-radius: 4px;

			/* Inside Auto Layout */

			flex: none;
			order: 0;
			flex-grow: 0;
			margin: 4px 0px;
		}
	}
</style>