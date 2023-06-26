<template>
    <div v-if="loading" class="fixed top-0 left-0 w-full h-full flex items-center justify-center bg-black bg-opacity-50">
    <div class="loader"></div>
  </div>
     <div v-if="error" class="text-red-500">{{ error }}</div>

  <div class="container w-full px-4 mx-auto sm:px-8">
        <div class="mb-4">
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" @click="showPostModal2">
          Create Branches
        </button>
        <button v-if="!isToken" class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded ml-2" @click="showPostModal">
         login
        </button>
      </div>
      <div class="py-8">
          <div class="px-4 py-4 -mx-4 overflow-x-auto sm:-mx-8 sm:px-8">
              <div class="inline-block w-full overflow-hidden rounded-lg shadow">
                <div v-if="data.length === 0" class="text-xl font-bold">
                  No data Yet or login to get data
                </div>
                  <table v-if="data.length>0" class="w-full leading-normal">
                      <thead>
                          <tr>
                              <th scope="col" class="px-5 py-3 text-sm font-normal text-left text-gray-800 uppercase bg-white border-b border-gray-200">
                                  Name
                              </th>
                              <th scope="col" class="px-5 py-3 text-sm font-normal text-center text-gray-800 uppercase bg-white border-b border-gray-200">
                                  city
                              </th>
                              <th scope="col" class="px-5 py-3 text-sm font-normal text-center text-gray-800 uppercase bg-white border-b border-gray-200">
                                 address
                              </th>
                              <th scope="col" class="px-5 py-3 text-sm font-normal text-left text-gray-800 uppercase bg-white border-b border-gray-200">
                                  edit
                              </th>

                               <th scope="col" class="px-5 py-3 text-sm font-normal text-left text-gray-800 uppercase bg-white border-b border-gray-200">
                                    delete
                                </th>
                          </tr>
                      </thead>
                      <tbody>
                          <tr v-for="(item, index) in data" :key="index">
                              <td class="px-5 py-3 text-sm bg-white border-b border-gray-200">
                                  <div class="flex items-center">
                                      <!-- <div class="flex-shrink-0">
                                          <a href="#" class="relative block">
                                              <img alt="profil" src="/images/person/8.jpg" class="mx-auto object-cover rounded-full h-10 w-10 "/>
                                          </a>
                                      </div> -->
                                      <div class="ml-3">
                                          <p class="text-gray-900 whitespace-no-wrap">
                                            {{ item.name }}
                                          </p>
                                      </div>
                                  </div>
                              </td>
                              <td class="px-5 py-3 text-sm bg-white border-b border-gray-200">
                                  <p class="text-gray-900 whitespace-no-wrap">
                                     {{ item.city }}
                                  </p>
                              </td>
                              <td class="px-5 py-3 text-sm bg-white border-b border-gray-200">
                                  <p class="text-gray-900 whitespace-no-wrap">
                                     {{ item.address }}
                                  </p>
                              </td>
                              <td class="px-5 py-3 text-sm bg-white border-b border-gray-200">
                                
  <button @click="showUpdateModal(item)" type="button" class="py-2 px-4 flex justify-center items-center  bg-blue-600 hover:bg-blue-700 focus:ring-blue-500 focus:ring-offset-blue-200 text-white w-full transition ease-in duration-200 text-center text-base font-semibold shadow-md focus:outline-none focus:ring-2 focus:ring-offset-2  w-12 h-12 rounded-lg ">
      <svg width="20" height="20" fill="currentColor" viewBox="0 0 1792 1792" xmlns="http://www.w3.org/2000/svg">
          <path d="M1344 1472q0-26-19-45t-45-19-45 19-19 45 19 45 45 19 45-19 19-45zm256 0q0-26-19-45t-45-19-45 19-19 45 19 45 45 19 45-19 19-45zm128-224v320q0 40-28 68t-68 28h-1472q-40 0-68-28t-28-68v-320q0-40 28-68t68-28h427q21 56 70.5 92t110.5 36h256q61 0 110.5-36t70.5-92h427q40 0 68 28t28 68zm-325-648q-17 40-59 40h-256v448q0 26-19 45t-45 19h-256q-26 0-45-19t-19-45v-448h-256q-42 0-59-40-17-39 14-69l448-448q18-19 45-19t45 19l448 448q31 30 14 69z">
          </path>
      </svg>
  </button>

                              </td>

                               <td class="px-5 py-3 text-sm bg-white border-b border-gray-200">
                                
    <button @click="showDeleteModal(item.id)"  type="button" class="py-2 px-4 flex justify-center items-center  bg-red-600 hover:bg-red-700 focus:ring-red-500 focus:ring-offset-blue-200 text-white w-full transition ease-in duration-200 text-center text-base font-semibold shadow-md focus:outline-none focus:ring-2 focus:ring-offset-2  w-12 h-12 rounded-lg ">
        <svg width="20" height="20" fill="currentColor" viewBox="0 0 1792 1792" xmlns="http://www.w3.org/2000/svg">
            <path d="M1344 1472q0-26-19-45t-45-19-45 19-19 45 19 45 45 19 45-19 19-45zm256 0q0-26-19-45t-45-19-45 19-19 45 19 45 45 19 45-19 19-45zm128-224v320q0 40-28 68t-68 28h-1472q-40 0-68-28t-28-68v-320q0-40 28-68t68-28h427q21 56 70.5 92t110.5 36h256q61 0 110.5-36t70.5-92h427q40 0 68 28t28 68zm-325-648q-17 40-59 40h-256v448q0 26-19 45t-45 19h-256q-26 0-45-19t-19-45v-448h-256q-42 0-59-40-17-39 14-69l448-448q18-19 45-19t45 19l448 448q31 30 14 69z">
            </path>
        </svg>
    </button>

                                </td>
                          </tr>
                      </tbody>
                  </table>
              </div>
          </div>
      </div>
  </div>


</template>

<script>
  import axios from 'axios';
  import Swal from 'sweetalert2';
export default {

  name: 'HelloWorld',


   data() {
    return {
      data: [],
      error: '',
      errorToast: '',
      isToken : '',
      loading: false
    };
  },
  created() {
    const token = localStorage.getItem('token');
       if (token) {
      this.isToken = token
    }
    this.fetchData(); // Automatically call fetchData when the component is created
  },
  methods: {
    fetchData() {
    this.loading = true
      const token = localStorage.getItem('token');
      if (token) {
        axios.defaults.headers.common['Authorization'] = `Bearer ${token}`;
      }
      axios
        .get('https://eduthon-api.delwathon.com/api/branches')
        .then((response) => {
          console.log(response)
          this.data = response.data.branches;
          this.fetchData
          this.loading = false
        })
        .catch((error) => {

          this.error = error.message;
          this.loading = false
        });
    },

   

    showPostModal() {
      Swal.fire({
        title: 'Login',
        html:
          '<input id="swal-input1" class="swal2-input" placeholder="Email">' +
          '<input id="swal-input2" class="swal2-input" type="password" placeholder="password">',
        showCancelButton: true,
        confirmButtonText: 'Login',
        preConfirm: () => {
          const email = document.getElementById('swal-input1').value;
          const password = document.getElementById('swal-input2').value;
          this.login(email, password);
        },
      });
    },
    login(email, password) {
      this.loading = true
      axios
        .post('https://eduthon-api.delwathon.com/api/login', { email, password })
        .then((res) => {
          console.log(res)
          // Creation successful, you can perform any necessary actions here
          const token = res.data.token;
          localStorage.setItem('token', token);
          this.fetchData(); // Refresh data after creation
          this.loading = false
        })
        .catch((error) => {
          this.error = error.message;
          this.loading = false
        });
    },

        showPostModal2() {
      Swal.fire({
        title: 'Create Branches',
        html:
          '<input id="swal-input1" class="swal2-input" placeholder="name">' +
          '<input id="swal-input2" class="swal2-input"  placeholder="short_name">' +
          '<input id="swal-input3" class="swal2-input" placeholder="Email">' +
          '<input id="swal-input4" class="swal2-input"  placeholder="phone">' +
          '<input id="swal-input5" class="swal2-input" placeholder="city">' +
          '<input id="swal-input6" class="swal2-input"  placeholder="address">' 
        ,
        showCancelButton: true,
        confirmButtonText: 'Create',
        preConfirm: () => {
          const name = document.getElementById('swal-input1').value;
          const short_name = document.getElementById('swal-input2').value;
          const email = document.getElementById('swal-input3').value;
          const phone = document.getElementById('swal-input4').value;
           const city = document.getElementById('swal-input5').value;
          const address = document.getElementById('swal-input6').value;
          this.create(email, name, short_name, phone, city, address);
        },
      });
    },
    create(email, name, short_name, phone, city, address) {
      this.loading = true
        const token = localStorage.getItem('token');
      if (token) {
        axios.defaults.headers.common['Authorization'] = `Bearer ${token}`;
      }
      axios
        .post('https://eduthon-api.delwathon.com/api/branches', {  email, name, short_name, phone, city, address,state_id: 25,
          local_government_id: 250, email_mask:'@dis.com', password_mask: "dis2012!" })
        .then((res) => {
          console.log(res)
          // Creation successful, you can perform any necessary actions here
         
          this.fetchData(); // Refresh data after 
          this.loading = false
        })
        .catch((error) => {
          console.log(error)
          this.error = error.response.data.message;
          this.loading = false
          this.showErrorToast(this.error);

        });
    },

    showErrorToast(message) {
      this.errorToast = message;
      setTimeout(() => {
        this.errorToast = '';
      }, 9000);
    },


        showUpdateModal(item) {
          Swal.fire({
            title: 'Update Data',
            html:
              `<input id="swal-input1" class="swal2-input" placeholder="name" value="${item.name}">` +
              `<input id="swal-input2" class="swal2-input"  placeholder="short_name" value="${item.short_name}">` +
          `<input id="swal-input3" class="swal2-input" placeholder="Email" value="${item.email}">` +
          `<input id="swal-input4" class="swal2-input"  placeholder="phone" value="${item.phone}">` +
          `<input id="swal-input5" class="swal2-input" placeholder="city" value="${item.city}">` +
          `<input id="swal-input6" class="swal2-input"  placeholder="address" value="${item.address}">` ,
        showCancelButton: true,
        confirmButtonText: 'Update',
        preConfirm: () => {
           const name = document.getElementById('swal-input1').value;
          const short_name = document.getElementById('swal-input2').value;
          const email = document.getElementById('swal-input3').value;
          const phone = document.getElementById('swal-input4').value;
          const city = document.getElementById('swal-input5').value;
          const address = document.getElementById('swal-input6').value;
          this.updateData(item.id, email, name, short_name, phone, city, address);
        },
      });
    },

    updateData(id, email, name, short_name, phone, city, address) {
       this.loading = true
      const token = localStorage.getItem('token');
      if (token) {
        axios.defaults.headers.common['Authorization'] = `Bearer ${token}`;
      }
      axios
        .put(`https://eduthon-api.delwathon.com/api/branches/edit/${id}`, {
          email, name, short_name, phone, city, address, state_id: 1,
          local_government_id: 1, email_mask: '@dis.com', password_mask: "dis2012!"
        })
        .then(() => {
          // Update successful, you can perform any necessary actions here
          console.log('Data updated successfully.');
          this.fetchData(); // Refresh the fetched data
          this.loading = false
        })
        .catch((error) => {
          this.error = error.message;
          this.loading = false
        });
    },
    showDeleteModal(id) {
        Swal.fire({
          title: 'Confirm Deletion',
          text: 'Are you sure you want to delete branch?',
          icon: 'warning',
          showCancelButton: true,
          confirmButtonColor: '#d33',
          cancelButtonColor: '#3085d6',
          confirmButtonText: 'Delete',
          preConfirm: () => {
            this.deleteData(id);
          },
        });
      },
  
    deleteData(id) {
        this.loading = true
        const token = localStorage.getItem('token');
        if (token) {
          axios.defaults.headers.common['Authorization'] = `Bearer ${token}`;
        }
        axios
          .delete(`https://eduthon-api.delwathon.com/api/branches/delete/${id}`)
          .then(() => {
            // Deletion successful, you can perform any necessary actions here
            console.log('Data deleted successfully.');
            this.fetchData(); // Refresh the fetched data
            this.loading = false
          })
          .catch((error) => {
            this.error = error.message;
            this.loading = false
          });
      },
  },

  
  

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .loader {
    border: 8px solid #f3f3f3; /* Light grey */
    border-top: 8px solid #3498db; /* Blue */
    border-radius: 50%;
    width: 60px;
    height: 60px;
    animation: spin 1.5s linear infinite;
  }

  @keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }

    /* ... existing styles ... */

  /* Error Toast styles */
  .error-toast {
    position: fixed;
    bottom: 20px;
    left: 50%;
    transform: translateX(-50%);
    padding: 12px 20px;
    background-color: #f44336; /* Red */
    color: #fff;
    border-radius: 4px;
    opacity: 0;
    transition: opacity 0.3s;
    animation: slideIn 0.3s, fadeOut 0.3s 2.7s;
  }

  @keyframes slideIn {
    from { bottom: -50px; }
    to { bottom: 20px; }
  }

  @keyframes fadeOut {
    from { opacity: 1; }
    to { opacity: 0; }
  }
</style>
