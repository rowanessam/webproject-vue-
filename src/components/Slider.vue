<template>
  <div id="app">
    <div id="view" :class="[{'collapsed' : collapsed}]" >
      <router-view/>
    
    </div>
    <sidebar-menu
      class="sidebar"
      :menu="menu"
    
      :collapsed="collapsed"
      @item-click="onItemClick"
      @collapse="onCollapse "
      
    />
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      menu: [
        {
          href: "/newprod",
          title: "New",
          icon: "fa fa-icons8-family-clothes-64"


        },
        {
          href: "/skirts",
          title: "Skirts",
          icon: "fa fa-code"
        },
        {
          href: "/blouses",
          title: "Blouses",
          icon: "fa fa-download"
        },
        {
          href: "/pants",
          title: "Pants",
          icon: "fa fa-download"
        },
        
        {
          href: "/coats",
          title: "Coats&Jackets",
          icon: "fa fa-download"
        },
        {
          href: "/sweatshirts",
          title: "Sweat-Shirts",
          icon: "fa fa-download"
        },
        {
          href: "/dresses",
          title: "Dresses",
          icon: "fa fa-download"
        },
        {
          href: "/blazers",
          title: "Blazers",
          icon: "fa fa-download"
        },
        
        {
          href: "/jumpsuits",
          title: "JumpSuits",
          icon: "fa fa-download"
        },
      
      ],
      collapsed: true
    };
  },
  methods: {
    onItemClick() {
      console.log("onItemClick");
    },
    onCollapse() {
      console.log("onCollapse");
      this.collapsed ;
    }
  }
};
</script>

<style scoped>
#view {
  padding-left: 350px;
  

}
#view.collapsed {
  padding-left: 50px;
}

.sidebar.v-sidebar-menu .vsm-arrow:after {
  content: "\f105";
  font-family: "FontAwesome";
  background-color:#ff006e;
  position: fixed;



}
.sidebar.v-sidebar-menu .collapse-btn:after {
  content: "\f07e";
  font-family: "FontAwesome";
}
</style>
