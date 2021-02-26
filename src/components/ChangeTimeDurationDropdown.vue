    <!-- =========================================================================================
    File Name: ChangeTimeDurationDropdown.vue
    Description: Change duration dropdown component
    ----------------------------------------------------------------------------------------
    Item Name: Vuexy - Vuejs, HTML & Laravel Admin Dashboard Template
      Author: Pixinvent
    Author URL: http://www.themeforest.net/user/pixinvent
========================================================================================== -->

<!-- :class="data.class" -->

<template functional>
    <vs-dropdown vs-trigger-click class="cursor-pointer" :class="data.staticClass">
        <small class="flex cursor-pointer">
          <span>过去7天</span>
          <feather-icon icon="ChevronDownIcon" svgClasses="h-4 w-4" class="ml-1" />
        </small>
        <vs-dropdown-menu class="w-32">
            <vs-dropdown-item @click="listeners.timeDurationChanged ? { timeDurationChanged: listeners.timeDurationChanged('last-28-days') } : null">过去1月</vs-dropdown-item>
            <vs-dropdown-item @click="listeners.timeDurationChanged ? { timeDurationChanged: listeners.timeDurationChanged('last-month') } : null">过去1年</vs-dropdown-item>
            <vs-dropdown-item @click="listeners.timeDurationChanged ? { timeDurationChanged: listeners.timeDurationChanged('last-year') } : null">全部</vs-dropdown-item>
        </vs-dropdown-menu>
    </vs-dropdown>
</template>
