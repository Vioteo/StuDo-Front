/* eslint-disable */
<template>
    <div class="box">
        <header>
            <div class="logoBlock d-flex">
                <div class="logo d-flex">
                    <div class="imgLogo">
                        <img src="../../src/assets/logo.png" height="50px" width="50px"/></div>
                    <div class="nameLogo">
                        StuDo
                    </div>
                </div>
            </div>
        </header>

        <transition name="popup">
            <div v-if="showPopup" class="blur_layer"  @click="back" />
        </transition>

        <transition name="popup">
            <popup v-if="showLogin" class="inFront" :viewName="message" @close="closePopup" />
        </transition>

        <div>
            <div class="menu" :class="blur">
                <input id="menu_toggle" type="checkbox" />
                <label id="menu_btn" for="menu_toggle">
                    <span></span>   
                </label>
                <div class="btnsMenu">
                    <div class="menuBarBut">
                        <a href="javascript: void(0);" @click="create">Создать объявление</a>
                    </div>
                    <div class="btnMenuItems d-flex">
                        <div class="btnActiv"></div>
                        <div class="pointers">
                            <router-link style="position: relative; color: white; opacity: 0.8;" to="/Logged">Все объявления</router-link>
                        </div>
                    </div>
                    <div class="btnMenuItems d-flex">
                        <div class="btnPassiv"></div>
                        <div class="pointers">
                            <router-link style="position: relative; color: white; opacity: 0.8;"  to="/MyLogged">Мои объявления</router-link>
                        </div>
                    </div>
                    <div class="btnMenuItems d-flex">
                        <div class="btnPassiv"></div>
                        <div class="pointers">
                            <router-link style="position: relative; color: white; opacity: 0.8;"  to="/Favorited">Закладки</router-link>
                        </div>
                    </div>
                </div>
            </div>
            <div class="row">
                <div class="col-4 firstCol" :class="blur">
                    <div class="fixedCol">
                        <div class="menuBar">
                            <div class="btnsMenu">
                                <div class="menuBarBut">
                                    <a href="javascript: void(0);" @click="create">Создать объявление</a>
                                </div>
                                <div class="btnMenuItems d-flex">
                                    <div class="btnActiv"></div>
                                    <div class="pointers">
                                        <router-link style="position: relative; color: white; opacity: 0.8;" to="/Logged">Все объявления</router-link>
                                    </div>
                                </div>
                                <div class="btnMenuItems d-flex">
                                    <div class="btnPassiv"></div>
                                    <div class="pointers">
                                        <router-link style="position: relative; color: white; opacity: 0.8;"  to="/MyLogged">Мои объявления</router-link>
                                    </div>
                                </div>
                                <div class="btnMenuItems d-flex">
                                    <div class="btnPassiv"></div>
                                    <div class="pointers">
                                        <router-link style="position: relative; color: white; opacity: 0.8;"  to="/Favorited">Закладки</router-link>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div id="clear"></div>
                <div class="col-4 mainArea">
                    <div class="postBlocks" v-for="post in filteredPosts" :key="post.id">
                        <transition name="popup">
                            <popup v-if="isShowing(post.id)" class="inFront" :viewName="'oneElem'" :id="post.id" @close="closePopup" />
                        </transition>
                        <div class="postBlock" :class="blur">
                            <div class="postTopBlock">
                                <button :id="post.id" v-if="isFavorite(post)" class="BookmarkBtn" @click="Bookmark(post.id)">
                                </button>
                                <button :id="post.id" v-if="!isFavorite(post)" class="BookmarkBtnIs" @click="Bookmark(post.id)">
                                </button>
                                <div class="blockTopForLogo">
                                    <i class="fa fa-ambulance" aria-hidden="true"></i>
                                </div>
                                <div class="titleForPost"><a href="javascript: void(0);" @click="showPost(post.id)">{{post.name}}</a>
                                </div>
                            </div>
                            <div class="postDownBlock">
                                <div class="textblockForPost">
                                    {{post.shortDescription}}
                                </div>
                                <div class="postdate">
                                    {{formatDate(new Date(post.beginTime))}} - {{formatDate(new Date(post.endTime))}}
                                </div>
                            </div>
                            <div style="color: honeydew" v-if="getter(post.lastComment,false)" class="CommentAuthorForPost">
                                Автор: {{getter(post.lastComment,false)}}
                            </div>
                            <div  v-if="getter(post.lastComment,false)" class="CommentblockForPost">
                                {{getter(post.lastComment,true)}}...
                            </div>
                        </div>
                    </div>
                </div>
                <div class="col-4 thirdCol" :class="blur">
                    <div class="fixedCol">
                        <div class="topMenu d-flex">
                            <div class="topMenuItems active">
                                <router-link style="position: relative; color: white; opacity: 0.8;" to="/Logged">Объявления</router-link>
                            </div>
                            <div class="topMenuItems">
                                <router-link style="position: relative; color: white; opacity: 0.8;" to="/Resumes">Резюме</router-link>
                            </div>
                            <div class="topMenuItems">
                                <router-link style="position: relative; color: white; opacity: 0.8;" to="/Profile">Профиль</router-link>
                            </div>
                        </div>
        
                        <div class="rightBlock">
                            <div class="rightBlock_block">
                                <div class="searchform d-flex">
                                    <input type="text" class="searchInput" v-model="query">
                                    <div class="searchLogo" @click="filterPosts(query)">
                                        <i class="fa fa-search" aria-hidden="true"></i>
                                    </div>
                                </div>
                                <div class="sortBlock">
                                    Сортировка
                                    <div class="sortItems">
                                        <div class="sortItem d-flex">
                                            <div class="sortItemsStatus sortItemsStatusActiv"></div>По дате создания
                                        </div>
                                        <div class="sortItem d-flex">
                                            <div class="sortItemsStatus"></div>Категории
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import router from "@/router";
    import axios from 'axios';
    import popup from './Popup';

    export default {
        name: "Logged",
        components: {
            popup: popup
        },
        props: ['id'],
        data() {
            return {
                rawHtml: {},
                posts: [],
                filteredPosts: [],
                comments: [],
                openedPost: -1,
                showPopup: false,
                showLogin: false,
                message: 'login',
                blur: ''
            };
        },
        methods : {
            getter(data, isText) {
                try {
                    if(isText) {
                        return data.text
                    }
                    else {
                        return data.author
                    }
                } catch (err) {
                    return false;
                }
            },
            isShowing(id) {
                if (this.openedPost === -1)
                    return false
                else if (this.filteredPosts[this.openedPost].id === id)
                    return true
                else
                    return false;
            },
            isFavorite(post) {
                return post.isFavorite
            },
            back() {
                router.push({query: ''});
                if (this.openedPost != -1) {
                    this.filteredPosts[this.openedPost].show = false;
                    this.openedPost = -1;
                    this.showPopup = false;
                    this.blur = '';
                }
            },
            create() {
                this.message = 'create';
                this.showPopup = true;
                this.showLogin = true;
                this.blur = 'blur_test';
            },
            formatDate(date) {
                var dd = date.getDate();
                if (dd < 10) dd = '0' + dd;
                var mm = date.getMonth() + 1;
                if (mm < 10) mm = '0' + mm;
                var yy = date.getFullYear();
                if (yy < 10) yy = '0' + yy;
                return dd + '.' + mm + '.' + yy;
            },
            Bookmark(a) {
                axios({
                    headers: {
                        'Authorization': "bearer " + this.$cookies.get("ACCESSTOKEN")
                    },
                    method: 'post',
                    url: process.env.VUE_APP_API + 'ad/bookmarks/' + a,
                    data: {}
                }).then(data => {
                    if(data)
                    var leftSection = document.getElementById(a);
                    leftSection.classList.replace('BookmarkBtnIs', 'BookmarkBtn');
                    this.$notify({
                        group: 'foo',
                        title: 'Пост добавлен в закладки'
                    });
                }).catch(error => {
                    if(error)
                        this.$notify({
                        group: 'foo',
                        title: 'Пост уже был добавлен в закладки'
                    });
                });
            },
            showPost(id) {
                router.push({query: {id: id}});
                for (var i = 0; i < this.filteredPosts.length; i++) {
                    if (this.filteredPosts[i].id === id) {
                        this.filteredPosts[i].show = true;
                        this.showPopup = true;
                        this.openedPost = i;
                        this.blur = 'blur_test';
                    }
                }
            },
            closePopup(e) {
                if (e === 'unauthorized') {
                    this.filteredPosts[this.openedPost].show = false;
                    this.openedPost = -1;

                    this.message = 'login';
                    this.showLogin = true;
                }
                else {
                    this.showPopup = false;
                    this.showLogin = false;
                    this.blur = '';

                    if (this.message === 'login')
                        router.go();
                }
            },
            filterPosts(query) {
                this.filteredPosts = this.posts.filter(function(post) {
                    if (post.name.toLowerCase().indexOf(query.toLowerCase()) > -1)
                        return true;
                    if (post.shortDescription.toLowerCase().indexOf(query.toLowerCase()) > -1)
                        return true;
                    return false;
                });
            }
        },
        mounted() {
            axios({
                headers: {
                    'Authorization': "bearer " + this.$cookies.get("ACCESSTOKEN")
                },
                method: 'get',
                url: process.env.VUE_APP_API + 'ad',
                data: {}
            }).then(data => {
                this.posts = data.data;
                this.filteredPosts = JSON.parse(JSON.stringify(data.data));
                for (let i = 0; i < this.filteredPosts.length; i++) {
                    this.filteredPosts[i].show = false;
                    this.comments.push(this.filteredPosts[i].lastComment);
                }
                if (this.id != '') {
                    for (var i = 0; i < this.filteredPosts.length; i++) {
                        if (this.filteredPosts[i].id === this.id) {
                            this.filteredPosts[i].show = true;
                            this.showPopup = true;
                            this.openedPost = i;
                            this.blur = 'blur_test';
                        }
                    }
                }
            }).catch(error => {
                // eslint-disable-next-line no-console
                if(error.response.status==401) {
                    this.message = 'login';
                    this.showPopup = true;
                    this.showLogin = true;
                    this.blur = 'blur_test';
                }
            });
        }
    }
</script>

<style scoped>
    .catBlock{
        width: 290px;
        margin-left: 19px;
        margin-top: 14px;
        color: #ACACAC;
        font-size: 16px;
    }
    .catBlock {
        border-radius: 0;
    }
    .countCat{
        text-align: right;
        position: absolute;
        right: 22px;
        font-size: 18px;
        color: #ACACAC;
    }
</style>