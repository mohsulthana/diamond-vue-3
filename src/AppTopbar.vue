<template>
<div class="layout-topbar">
  <div class="topbar-left">
    <!-- <a tabindex="0" class="menu-button" @click="onMenuButtonClick">
                <i class="pi pi-chevron-left"></i>
            </a> -->

    <router-link to="/" class="horizontal-logo">
      <img id="logo-horizontal" src="assets/layout/images/logo-dark.svg" alt="diamond-layout" />
    </router-link>

    <!-- <div class="layout-breadcrumb viewname" style="text-transform: uppercase">
      <template v-if="$route.meta.breadcrumb">
        <span>{{$route.meta.breadcrumb[0].label}}</span>
      </template>
    </div> -->

    <!-- <span class="topbar-separator"></span> -->

    <div class="layout-breadcrumb" style="text-transform: uppercase; margin-left: 10px">
      <Dropdown v-model="dropdownValue" :options="dropdownValues" optionLabel="name" placeholder="Location" />
    </div>

    <img id="logo-mobile" class="mobile-logo" src="assets/layout/images/logo-dark.svg" alt="diamond-layout" />
  </div>

  <AppMenu :model="menu" :layoutMode="layoutMode" :active="menuActive" :mobileMenuActive="staticMenuMobileActive" @menu-click="onMenuClick" @menuitem-click="onMenuItemClick" @root-menuitem-click="onRootMenuItemClick"></AppMenu>

  <div class="layout-mask modal-in"></div>

  <div class="topbar-right">
    <ul class="topbar-menu">
      <li class="profile-item" :class="{ 'active-menuitem ': topbarNotificationMenuActive }">
        <a href="#" tabindex="0" @click="onTopbarNotificationMenuButtonClick">
          <span class="office-name">Main Office 12th Street</span>
        </a>
      </li>

      <li class="profile-item" :class="{ 'active-menuitem fadeInDown': topbarUserMenuActive }">
        <a href="#" @click="onTopbarUserMenuButtonClick">
          <img src="assets/demo/images/avatar/profile.jpg" alt="diamond-layout" class="profile-image" />
          <span class="profile-name">Hi, Amelia Stone</span>
        </a>
        <ul class="profile-menu fade-in-up">
          <li>
            <a href="#">
              <i class="pi pi-user"></i>
              <span>Profile</span>
            </a>
          </li>
          <li>
            <a href="#">
              <i class="pi pi-cog"></i>
              <span>Settings</span>
            </a>
          </li>
          <li>
            <a href="#">
              <i class="pi pi-calendar"></i>
              <span>Calendar</span>
            </a>
          </li>
          <li>
            <a href="#">
              <i class="pi pi-inbox"></i>
              <span>Inbox</span>
            </a>
          </li>
          <li>
            <a href="#">
              <i class="pi pi-power-off"></i>
              <span>Logout</span>
            </a>
          </li>
        </ul>
      </li>

      <li class="right-sidebar-item">
        <a href="#" tabindex="0" @click="onRightMenuClick">
          <i class="pi pi-cog"></i>
        </a>
      </li>
    </ul>
  </div>
</div>
</template>

<script>
import AppMenu from "./AppMenu";
export default {
  name: "AppTopbar",
  emits: ["menu-click", "menuitem-click", "root-menuitem-click", "menu-button-click", "search-click", "topbar-notification", "topbar-user-menu", "right-menubutton-click"],
  props: {
    topbarNotificationMenuActive: Boolean,
    topbarUserMenuActive: Boolean,
    layoutMode: String,
    menu: Array,
    menuActive: Boolean,
    staticMenuMobileActive: Boolean
  },
  data() {
    return {
      items: [],
      dropdownValues: [{
          name: 'New York',
          code: 'NY'
        },
        {
          name: 'Rome',
          code: 'RM'
        },
        {
          name: 'London',
          code: 'LDN'
        },
        {
          name: 'Istanbul',
          code: 'IST'
        },
        {
          name: 'Paris',
          code: 'PRS'
        }
      ],
      dropdownValue: null,
    };
  },
  components: {
    AppMenu
  },
  unmounted() {
    if (this.subscription) {
      this.subscription.unsubscribe();
    }
  },
  methods: {
    onMenuClick(event) {
      this.$emit("menu-click", event);
    },
    onMenuItemClick(event) {
      this.$emit("menuitem-click", event);
    },
    onRootMenuItemClick(event) {
      this.$emit("root-menuitem-click", event);
    },
    onMenuButtonClick(event) {
      this.$emit("menu-button-click", event);
    },
    onSearchClick(event) {
      this.$emit("search-click", event);
    },
    onTopbarNotificationMenuButtonClick(event) {
      this.$emit("topbar-notification", event);
    },
    onTopbarUserMenuButtonClick(event) {
      this.$emit("topbar-user-menu", event);
    },
    onRightMenuClick(event) {
      this.$emit("right-menubutton-click", event);
    },
    isMobile() {
      return window.innerWidth <= 1091;
    }
  }
};
</script>

<style lang="scss" scoped>
.profile-item {
  border-left: none !important;
  border-right: none !important;

  a {
    span:first-child.office-name {
      color: orange;
      font-size: 15px;
    }

    span.profile-name {
      color: white;
    }
  }
}

.layout-topbar {
  background-color: #333333;
  color: white;
}
.p-placeholder.p-dropdown-label.p.inputtext {
  color: white !important;
}
.p-dropdown {
    background-color: transparent;
    color: white;
    border: none;
}
</style>
