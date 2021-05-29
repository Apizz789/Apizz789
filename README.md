- 👋 Hi, I’m @Apizz789
- 👀 I’m interested in Brill Chatkul (Just Real)
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Apizz789/Apizz789 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">

    <title>Github portfolio generator with your main languages</title>
    <meta name="description" content="Github portfolio: Get a chart with the main languages within your repositories and your total number of stars.">
    
    <link rel="canonical" href="http://isradeleon.com/github-portfolio.html">

    <meta property="og:url" content="http://isradeleon.com/github-portfolio.html">
    <meta property="og:type" content="website">
    <meta property="og:image:type" content="image/png">
    <meta property="og:image:width" content="640">
    <meta property="og:image:height" content="320">

    <meta property="og:title" content="Github portfolio generator with your main languages">
    <meta property="og:description" content="Github portfolio: Get a chart with the main languages within your repositories and your total number of stars.">
    <meta property="og:image" content="http://isradeleon.com/github-portfolio.png">

    <meta name="twitter:card" content="summary_large_image">
    <meta name="twitter:site" content="@isradeleon">
    <meta name="twitter:creator" content="@isradeleon">

    <meta name="twitter:title" content="Github portfolio generator with your main languages">
    <meta name="twitter:description" content="Github portfolio: Get a chart with the main languages within your repositories and your total number of stars.">
    <meta name="twitter:image" content="http://isradeleon.com/github-portfolio.png">

    <link rel="stylesheet" href="https://cdn.statically.io/gh/isradeleon/coraline/0.5.3/coraline-v0.5.3/coraline.min.css">
    <link href="https://cdn.statically.io/gh/isradeleon/flexboxlayout/1.0.0/production/flexboxlayout.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.9.0/css/all.min.css">
    
    <style>
        .hidden{
            display: none;
        }
        .spin-forever{
            animation-name: spin;
            animation-duration: 1000ms;
            animation-iteration-count: infinite;
            animation-timing-function: linear; 
        }
        .link:hover{
            background: transparent;
        }
        @keyframes spin {
            from {
                transform:rotate(0deg);
            }
            to {
                transform:rotate(360deg);
            }
        }
        .repository{
            padding: 10px;
            height: 100%;
        }
    </style>
</head>
<body>
    <div style="position: fixed; top: 0; bottom: 0; right: 0; left: 0;" id="particles-js"></div>
    <main>
        <div v-if="!loading && ready">
       <!--  <div v-if="user.length > 0 && !loading"> -->
            <nav class="navbar fixed" style="border: none; background-color: rgba(255, 255, 255, 0.98)">
        
                <!-- This link will stay here on mobile and tablet -->
                <a class="link text-size-s" href="#top">{{user}}</a>
            
                <!-- CSS animated menu icon -->
                <input class="menu-toggle" type="checkbox" id="menu1">
                <label style="margin-left: auto;" class="burger-btn" for="menu1">
                    <span class="burger-icon"></span>
                </label>
        
                <!-- This content will be responsive on mobile and tablet -->
                <div class="navbar-content text-size-s">
                    <div class="navbar-end">
                        <a class="link" href="#languages">
                            Languages
                        </a>
                        <a class="link" href="#repositories">
                            Repositories
                        </a>
                    </div>
                </div>
            
            </nav>

            <div id="top" class="site-section white" style="background: transparent;">

                <div class="container below-navbar text-center">
                    <div class="circular-img profile" :style="{ backgroundImage: 'url('+object.avatar_url+')' }"></div>
                    <h1 class="main-title">{{object.name ? object.name : object.login}}</h1>
                    <p class="below-title">{{object.bio}}</p>
                    <p class="below-title">
                        <i class="fa fa-users"></i> Followers: {{object.followers}} | 
                        <i class="fa fa-star"></i> Total stars: {{totalStars}}
                    </p>
                </div>
            </div>

            <div id="languages" class="site-section">
                <div class="container below-navbar text-center">
                    <h1>Main languages</h1>
                    <p class="below-title">Total: {{Object.keys(languages).length}}</p>
                    <template>
                        <div>
                            <apexchart width="100%" style="max-width: 600px; margin: auto;" type="donut" :options="options" :series="series"></apexchart>
                        </div>
                    </template>
                </div>
            </div>

            <div id="repositories" class="site-section white">
                <div class="container below-navbar">
                    <h1 class="text-center">Repositories</h1>
                    <p class="text-center below-title">Total: {{repositories.length}}</p>
                    <div class="grid">
                        <div v-for="repo in listing" class="col-4">
                            <div class="repository flex column">
                                <a target="_blank" :href="repo.html_url" class="text-size-6 text-bold">
                                    {{repo.name}}
                                </a>
                                <small>{{repo.description}}</small>
                                <hr>
                                <div>
                                    <strong v-if="repo.language" class="tag small rounded">
                                        {{repo.language}}
                                    </strong>
                                    <strong v-if="repo.stargazers_count" class="tag small rounded">
                                        <i class="far fa-star"></i> {{repo.stargazers_count}}
                                    </strong>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="text-center">
                        <button v-on:click="showAll()" v-if="!showing && repositories.length > 9" class="btn small text-secondary rounded">
                            <i class="fa fa-eye"></i> Show all
                        </button>
                    </div>
                </div>
            </div>

            <footer style="background: white; position: relative;">
                <div class="container text-size-s">
                    <p>
                        <a target="_blank" href="https://github.com/isradeleon/github-portfolio">
                            <i class="fab fa-github"></i> Github repository
                        </a><br>
                        Made with <i class="far fa-heart"></i> by <a target="_blank" href="https://github.com/isradeleon">@isradeleon</a>
                    </p>
                </div>
            </footer>

        </div>
    
        <div v-if="loading">
            <div class="site-section">
                <div class="container flex items-center justify-center column">
                    <i class="fa fa-spinner spin-forever"></i>
                    Loading...
                </div>
            </div>
        </div>
    
        <div v-if="!ready && !loading">
            <div class="site-section">
                <div class="container flex items-center justify-center column">
                    <div style="width: 100%;" class="text-center">
                        <h1>Github portfolio</h1>
                        <p class="below-title text-gray">Type the github username to generate a portflio for that profile:</p>
                        <input v-model="user" class="rounded full-width" placeholder="github_username" style="max-width: 400px;" type="text">
                        <br>
                    </div>
                    <button v-on:click="loadUserPortfolio()" class="btn rounded primary small inverted full-width" style="max-width: 400px;">
                        Generate
                    </button>
                </div>
            </div>
        </div>
    </main>

    <script src="https://cdn.jsdelivr.net/npm/particles.js@2.0.0/particles.min.js"></script>
    <script>
        particlesJS.load('particles-js', 'particles.json', function() {
            console.log('callback - particles.js config loaded');
        });
    </script>
    <script src="https://cdn.jsdelivr.net/npm/apexcharts"></script>
    <script src="https://cdn.jsdelivr.net/npm/vue-apexcharts"></script>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.6.0"></script>
    <script>
        (function(){
            function getParameterByName(name) {
                var match = RegExp('[?&]' + name + '=([^&]*)').exec(window.location.search);
                return match && decodeURIComponent(match[1].replace(/\+/g, ' '));
            }

            Vue.component('apexchart', VueApexCharts)
            var vue = new Vue({
                el:"main",
                data:{
                    loading: false,
                    user: '',
                    object: {},
                    ready: false,
                    showing: false,
                    languages: {},
                    options: {
                        labels: [],
                        plotOptions: {
                            pie: {
                                donut: {
                                    labels:{
                                        show: true,
                                        value: {
                                            formatter: function (val) {
                                                return val + (val > 1 ? " repositories":" repository");
                                            }
                                        }
                                    }
                                }
                            }
                        }
                    },
                    series: [],
                    repositories: [],
                    listing: [],
                    totalStars: 0
                },
                methods:{
                    showAll(){
                        this.listing = this.repositories
                        this.showing = true
                    },
                    loadUserPortfolio(){
                        console.log(window.location.host)
                        window.location.href = '?user='+this.user;
                    },
                    getUserData(){
                        console.log(this.user)
                        this.loading = true;

                        this.ready = true;

                        fetch( "https://api.github.com/users/"+this.user)
                        .then(response => response.json())
                        .then(data => {
                            console.log(data);
                            if(data.login){
                                this.object = data;
                                this.getUserRepos()
                            }else{
                                window.location.href = window.location.href.split('?')[0];
                            }
                        });
                    },
                    getUserRepos(){
                        fetch( "https://api.github.com/users/"+this.user+"/repos?sort=updated")
                        .then(response => response.json())
                        .then(data => {
                            console.log(data);
                            this.repositories = data;

                            if (this.repositories.length > 9) {
                                this.listing = this.repositories.slice(0,9)
                                this.listing.slice(0,9)
                            }else{
                                this.listing = this.repositories
                            }

                            for (let i = 0; i < data.length; i++) {
                                const repo = data[i];
                                this.totalStars+=repo['stargazers_count']
                                if(repo.language){
                                    if(this.languages.hasOwnProperty(repo.language)){
                                        this.languages[repo.language]++
                                    }else{
                                        this.languages[repo.language] = 1
                                    }
                                }
                            }
                            for (const key in this.languages) {
                                this.options.labels.push(key)
                                this.series.push(this.languages[key])
                            }
                            this.loading = false;
                            console.log(this.languages)
                        });
                    },
                    setUser(user){
                        this.user = user
                        this.getUserData()
                    }
                }
            })

            var user = getParameterByName("user");
            if(user){
                vue.loading = true
                vue.setUser(getParameterByName("user"));
            }

        })();
    </script>
</body>
</html>
