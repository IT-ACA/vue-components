<template>
  <v-container style="margin-top:-20px!important;" 
    grid-list-lg class="mx-0 pa-3 bg-surface-variant" mr-20 ml-20
  >
    <v-row style="align-items:center;margin-bottom:0px;backgroud-color: teal" no-gutters>  
      <h1 class="page-title" style="color:rgb(137 135 135);">
        <v-icon style="font-size: 4px">mdi-home</v-icon>
        Home</h1>
      <v-spacer></v-spacer>
      <h5 class="grey--text">
        {{ new Date().toLocaleDateString(locale, { weekday: 'short' }) }}, {{  new Date().toLocaleDateString(locale, { month: 'short' }) }} {{  new Date().getDate() }}
       <!-- {{ currentTime }} -->
      </h5>
    </v-row>



  <!-- <v-container id="dashboard" fluid grid-list-lg class="mx-0 pa-3"> -->
    <!-- <span style="color: red; display: inline-block">dashboard-classes-prep branch</span><br> -->
    <!-- <span>{{ label }}</span> -->
      <!-- <span>CHECK IF CAN USE OMIT in FMS API TO ONLY RETURN RECORDS THAT ARE NOT IN LOCAL STORAGE OR VUEX</span>
      <span>Check timestamps against stored newest/oldest timestamp in Vuex and use omit in query?</span> -->
      <!-- <pre>
        {{ notes.length }} notes
      </pre> -->
      <!-- <pre>
        number of classes {{  getAllClasses2Day.length }} 
        {{  getAllClassesToday }}
      </pre> -->

      <!-- <div style="border:1px solid #565656;border-radius:4px;padding:10px;border-bottom:30px;">
        <p>Dev logging now</p>
        <br> 
        <label for="current-branch">Current Branch: </label>Dev
        <br>
        Att due count : {{ classesWithIncompleteAttendance.length }}
        {{ API_msg }}
        App last updated: {{ this.lastUpdated }}
      </div> -->

  <!-- <v-alert v-if="updateEvent"
    v-model="submitAlertToggle"
    dense
    text
    type="success" dismissible transition="fade-transition"
    v-onchange="!submitAlertToggle"
  >
    Attendance submitted successfully for class with {{ updatedEvent.name }} on {{ updatedEvent.displayDate }}
  </v-alert> -->
<!--   
    <v-alert v-if="!notes.length" dense
      border="left"
      outlined
      type="info" close-text="Close Alert" 
          v-model="showUpdateAlert" dismissible @input="closedAlert($event)">
      Your schedule has been updated. Please see the Schedule Details section for more information.
    </v-alert> -->

    <!-- HERO -->
    <!-- <v-row style=""
    no-gutters>   -->
      <!-- <v-col> -->

        
      <!-- <v-row style="margin-bottom:10px;align-items:center;padding: 20px" no-gutters>
        <h1 class="page-title" style="color:rgb(113 116 115);font-size:24px">Dashboard</h1>
        <span v-show="viewingAsAdmin">
         <v-chip
            class="ma-6"
            color="blue"
            small
            label
            text-color="#d9e7f5"
            style="border: 0px solid #055deb;"
          >
            Admin Mode
          </v-chip>
        </span>
        <v-spacer></v-spacer>
        <h5 style="color:rgb(134 137 136) !important;">
          {{ new Date().toLocaleDateString(locale, { weekday: 'long' }) }}, 
          {{ new Date().toLocaleDateString(locale, { month: 'long' }) }} 
          {{ new Date().getDate() }}
        </h5>
      </v-row> -->



        <!-- </v-col> -->
      <!-- <v-col class="text-right" style="margin-top:-20px;"></v-col> -->
      <!-- {{ missingDataAlert }} -->

    <!-- </v-row> -->
    <v-alert v-if="missingDataAlert.length > 0"
      type="info"
      color="rgb(74 143 150)"
      dismissible
    >
      Some classes may be missing information. Please review and contact your course coordinator if necessary.  
    </v-alert>


  <div class="tabs">
    <v-tabs background-color="white" style="border-bottom: 1px solid lightgrey;">
      <v-tabs-slider color="#47b4d5"></v-tabs-slider>
      <v-tab v-for="(tab,index) in tabs" :key="index" @click="currentTab = index" 
      style="color:rgb(6 119 152);" background-color="teal darken-3">
        <v-icon left style="color:rgb(6 119 152); !important">
          {{ tab.icon }}
        </v-icon>
        <!-- <v-icon>mdi-phone</v-icon> -->
        {{ tab.title }}
      </v-tab>
    </v-tabs>
    
    <!-- CONTENT -->
    <div class="tab-content">
      <!-- Overview -->
      <div v-show="currentTab === 0" class="tab0">
        <v-col style="margin-bottom:10px;
          align-items:center;
          padding: 20px;
          /* border: 2px solid rgb(195 192 192 / 40%);  */
          /* border-radius: 5px; */
          background-color: #fefefe;
          /* box-shadow: black 14px; */
          /* box-shadow:rgb(208 208 208) 0px 0px 16px -3px;  */
          border-top: 0px solid #3a75b0;"
          no-gutters
        >
        <!-- <p> {{ isAdmin }} </p> -->
        <!-- <template v-show="isAdmin"> -->
        <!-- <p v-show="isAdmin">You are <b>viewing</b> as {{ user.firstname }} {{ user.lastname }}.</p> -->
        <!-- <p v-show="isAdmin">You are <b>viewing</b> as {{ user.teacher_name }}.</p> -->
        <p v-show="viewingAsAdmin">You are currently viewing in <b>admin mode</b>  as {{ viewingAsFullName }}.</p>

        <!-- </template> -->

        <!-- <p v-show="!viewingAsAdmin"> back, {{ user.teacher_name }}.</p> -->
        <h2 style="color: rgb(129 126 126);" v-show="!viewingAsAdmin">Hello, {{ userFirstName }}.</h2>
        <p>Please review your schedule and class updates below.</p>

        
        <!-- <p v-show="!viewingAsAdmin">You are signed in as {{ user.firstname }} {{ user.lastname }}.</p> -->

        <p>Current Test Date: {{ fakeNowDay }} </p>
        <!-- partials is broken ?? -->
        <!-- <p> 
          {{ partials.length }} <span v-if="partials.length > 1">classes have</span>
          <span v-else>class has</span>  incomplete attendance
        </p> -->
    
  <v-layout row wrap style="margin-bottom: 5px;">
  <!-- WIDGETS -->
    <v-flex
      md4
      sm12
      xs12
    >
      <v-card :class="" elevation="2" 
        style="padding: 12px;">
          <v-list-item>
            <v-list-item-action class="single-widget-icon-wrap">
              <!-- <v-btn icon>
                <v-icon color="grey lighten-3">mdi-information</v-icon>
              </v-btn> -->
              <!-- <v-list-item-avatar style="
                padding: 15px;"> -->
                <v-icon color="white" 
                  style="background-color: rgb(1 56 222 / 77%);
                  padding: 15px;
                  border-radius: 50%;
                  font-size: 36px;"
                >
                mdi-school
              </v-icon> 
            <!-- </v-list-item-avatar> -->
            </v-list-item-action>

            <!--  v-for="item in items2"
          :key="item.title"-->
            <v-list-item-content class="widget-data">
              <v-list-item-title class="widget-title" v-text="getAllClassesToday.length" style="color:rgb(93 90 90);"></v-list-item-title>
              <v-list-item-subtitle class="widget-text" style="color:rgb(137 137 137);">
                Classes Today
              </v-list-item-subtitle>
              <!-- <br /> -->
            </v-list-item-content>

          
          </v-list-item>
      </v-card>
    </v-flex>

    <v-flex
      md4
      sm12
      xs12
    >
      <v-card elevation="2" 
        style="background-color: #fff;
        padding: 10px;">
          <v-list-item>
            <v-list-item-action class="single-widget-icon-wrap">
              <!-- <v-btn icon>
                <v-icon color="grey lighten-3">mdi-information</v-icon>
              </v-btn> -->
              <!-- <v-list-item-avatar style="
                padding: 15px;"> -->
                <v-icon color="white" style="background-color: rgb(250 86 36);
                padding: 15px;
                border-radius: 50%;
                font-size: 36px;">
                mdi-alert-circle-outline
              </v-icon> 
            <!-- </v-list-item-avatar> -->
            </v-list-item-action>
            <!--  v-for="item in items2"
          :key="item.title"-->
            <v-list-item-content class="widget-data">
              <v-list-item-title class="widget-title" v-text="classesWithIncompleteAttendance.length" style="color:rgb(93 90 90);"></v-list-item-title>
              <v-list-item-subtitle class="widget-text" style="color:rgb(137 137 137);">
                {{ classesWithIncompleteAttendance.length === 1 ? 'Attendance Due' : 'Attendance Due' }}                
              </v-list-item-subtitle>
              <!-- <br /> -->
            </v-list-item-content>


          </v-list-item>
      </v-card>
    </v-flex>

    <v-flex
      md4
      sm12
      xs12
      >
        <v-card elevation="2" 
          style="background-color: #fefefe;
          padding: 10px;">
            <v-list-item>
              <v-list-item-action class="single-widget-icon-wrap">
                <!-- <v-btn icon>
                  <v-icon color="grey lighten-3">mdi-information</v-icon>
                </v-btn> -->
                <!-- <v-list-item-avatar style="
                  padding: 15px;"> -->
                  <v-icon color="white" style="background-color: rgb(4 165 189);
                  padding: 15px;
                  border-radius: 50%;
                  font-size: 36px;">
                  mdi-calendar-month
                </v-icon> 
              <!-- </v-list-item-avatar> -->
              </v-list-item-action>
              <!--  v-for="item in items2"
            :key="item.title"-->
              <v-list-item-content class="widget-data">
                <v-list-item-title class="widget-title" v-text="getNotes.length" style="color: rgb(93 90 90);"></v-list-item-title>
                <v-list-item-subtitle class="widget-text" style="color: rgb(137 137 137);">Schedule updates</v-list-item-subtitle>
                <!-- <br /> -->
              </v-list-item-content>


            </v-list-item>
        </v-card>
    </v-flex>
  </v-layout>

    
    
    
  </v-col>

      </div>
      <!-- updates -->
      <div v-show="currentTab === 1" class="tab1">
        <!-- SCHEDULE UPDATES SECTION -->
        <div v-show="true">
          <v-row no-gutters style="background: transparent; margin-bottom: 0px;
            padding: 0px;
            border-radius: 0px 0px 0px 0px;
            border-bottom: 3px solid #3a75b0;
            padding-bottom: 10px;"
            >
            <!-- <h2 class="mb-1 font-weight-medium" 
              style="font-size: 22px;
              color: rgb(107 107 109);
              letter-spacing: 0.19px;"
            >
            <v-icon style="padding: 4px;
              background-color: rgb(224 224 224);
              border-radius: 8px;
              font-size: 28px;
              margin-right: 3px;
              color: rgb(99 97 97);">
                mdi-calendar-month
            </v-icon> 
                Schedule Updates
            </h2> -->
          </v-row>
          <!-- {{ getNotes.length }} -->
          <div v-if="getNotes.length > 0" class="text-center updates-table" 
            style="border: 1px solid #e3e3e3;box-shadow: rgb(196 198 200) 0px 0px 6px -2px;">
            <!-- {{ getNotes[0] }} -->
            <template>
              <v-data-table
                :headers="updatesHeaders"
                :items="getNotes"
                :pagination.sync="schedulesPagination"
              >
                ...
              </v-data-table>
              <!-- <v-pagination
                v-model="schedulePagination.page"
                :length="schedulePagination.pages"
              /> -->
            </template>
            <!-- 
            <v-data-table
              :headers="updatesHeaders"
              :items="getNotes"
              item-key="name"
              :search="search"
              :page.sync="page"
              :items-per-page="itemsPerPage"
              hide-default-footer>
            </v-data-table>
            <v-pagination
              v-model="page"
              :length="2"
            >  
            </v-pagination> -->
          </div>
          <v-row no-gutters style="text-align: center;margin-bottom: 30px;">
            <v-col v-if="getNotes.length < 1" style="padding: 20px;background-color: #fff;">
              <!-- <v-icon style="padding: 10px;
                background-color: rgb(224 224 224);
                border-radius: 8px;
                font-size: 38px;
                margin-bottom: 10px;
                color: #7070708c;">mdi-calendar-month</v-icon> -->

              <div style="color: rgb(144 141 141);
                font-size: 24px;">
                <small style="font-style: italic">
                  Schedule is up-to-date
                </small>
              </div>
            </v-col>  
            <v-col v-else>
              <!-- <div> -->
                <!-- {{ getNotes }} -->
      
              <!-- </div> -->
            </v-col>
          </v-row>
        </div>

      </div>

      <!-- Attendance Due Tab -->
      <div v-show="currentTab === 2" class="tab2">
        <v-row no-gutters v-if="classesWithIncompleteAttendance.length < 1" 
          style="text-align: center;margin-bottom: 30px;"
        >
          <v-col style="padding: 20px;background-color: #f0f0f0;">
            <v-icon style="padding: 10px;
              background-color: rgb(224 224 224);
              border-radius: 8px;
              font-size: 38px;
              margin-bottom: 10px;
              color: #7070708c;"
            >mdi-check</v-icon>

            <div style="color: rgb(144 141 141);
              font-size: 24px;">
              Attendance is up-to-date
            </div>
          </v-col>  
        </v-row>

        <template v-else 
          style="margin-bottom: 150px !important;border: 1px solid red;"
        >
          <p>The following classes require attendance.</p>
          <!-- <v-hover v-slot="{ hover }"> -->
          <v-card v-for="(item,index) in classesWithIncompleteAttendance" 
            :key="index"
            :elevation="hover ? 6 : 3"
            :class="{ 'on-hover': hover }"
            @click="attendanceForm(item)" 
            style="margin-bottom: 30px !important;
            border-left: 5px solid #41c14d;"
          >
            <v-layout class="pa-3 project" style="margin-top: 4px">
              <v-flex xs3 sm4 md2>
                <!-- <div class="caption grey--text">Date</div> -->
                <!-- <div>
                  <ul style="list-style:none;padding:0px">
                    <li style="list-style:none;">{{ formatDate(item['fieldData']['scheduleDate'])[0] }}, {{ formatDate(item['fieldData']['scheduleDate'])[1] }}</li>
                    <li style="list-style:none;">{{ formatDate(item['fieldData']['scheduleDate'])[2] }}</li>
                  </ul>
                </div> -->
<div class="calendar-card">
  <div class="calendar-card-month">{{ formatDate(item['fieldData']['scheduleDate'])[1]}}</div>
  <div class="calendar-card-date">{{ formatDate(item['fieldData']['scheduleDate'])[1] }}</div>
  <div class="calendar-card-day">{{ formatDate(item['fieldData']['scheduleDate'])[0] }}</div>
</div>

<!-- <div class="card__date">
  <div class="date__container">
    <div class="month">APR</div>
    <div class="day">06</div>
    <div class="weekday">THU</div>
  </div>
  <div class="time">2:00 PM - 3:00 PM</div>
</div> -->
              </v-flex>

              <v-flex xs3 sm4 md2>
                <!-- <div class="caption grey--text">Client</div> -->
                <!-- <div>Client name</div> -->
                <span v-if="item['fieldData']['class_reg_students_CLIENTS::clientName']"> {{ item['fieldData']['class_reg_students_CLIENTS::clientName'] }}</span>
                <span v-else>N/A</span>
                <span v-show="item['portalData']['class_ATTENDANCES'].length >= 1">
                  <br>
                  <small style="color:orange;">Partially Complete</small>
                </span>
              </v-flex>

              <v-flex xs7 md6>
                <div class="caption grey--text">Student/Group</div>
                <div>
                  <span v-if="item['portalData']['class_REGISTRATIONS'].length === 1">   
                    {{ item['portalData']['class_REGISTRATIONS'][0]['class_reg_STUDENTS::firstName'] }} {{ item['portalData']['class_REGISTRATIONS'][0]['class_reg_STUDENTS::lastName'] }}
                  </span> 
                  <span v-if="!item.groupNo && item['portalData']['class_REGISTRATIONS'].length !== 1">
                    <!-- No data - please contact course coordinator -->
                    {{ item['fieldData']['SCHEDULES::groupName'] }}
                  </span>
                  <!-- <span v-if="item.groupNo">
                    - Group {{ item.groupNo }}
                  </span> -->
                </div>                     
              </v-flex>

              <v-flex xs2 sm4 md2 style="justify-content: center;
                text-align: right;
                align-items: center;
                margin-top: 10px;"
              >
                <v-btn
                  @click="attendanceForm(item)"
                  class="mx-0"
                  fab
                  small
                  color="rgb(243 174 29)"
                >
                  <v-icon style="color:white">
                    mdi-chevron-right
                  </v-icon>
                </v-btn>
              </v-flex>
            </v-layout>
            <!-- <v-divider></v-divider> -->
          </v-card>
        <!-- </v-hover> -->
        </template>

        
      </div>

      <!-- Schedules -->
      <div v-show="currentTab === 3" class="tab2">
      </div>
    </div>
  </div>

  


    <!-- {{ someComputed }} -->

  <!-- <v-row style="margin-bottom:10px;align-items:center" no-gutters>
    <v-card
      class=""
      max-width="600"
      outlined
    >
      <v-list-item three-line>
        <v-list-item-content>
          <div class="text-overline mb-4">
            NEXT CLASS
          </div>
          <v-list-item-title class="text-h5 mb-1">
            Class Name 
          </v-list-item-title>
          <v-list-item-subtitle>Date & Time</v-list-item-subtitle>
        </v-list-item-content>

        <v-list-item-avatar
          tile
          size="80"
          color="grey"
        ></v-list-item-avatar>
      </v-list-item>

      <v-card-actions>
        <v-btn
          outlined
          rounded
          text
        >
          Calendar
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-row> -->



      <!-- DEV OUTPUT FOR DEBUGGIN -->
      <!-- <v-row style="border:1px solid #555">
        <v-col cols="6">
          <v-title>Development Output</v-title>
          <div style="max-width:100%;overflow:;padding:20px;">
          {{ allClasses.length }} classes in this period
            <pre>
              {{ allClasses[13] }}
            </pre> 
            <ul>
              <li v-for="(i, index) in classesWithIncompleteAttendance" :key='index'>
                {{ i }}
              </li>
            </ul>
          </div>
        </v-col>
        <v-col cols="6">
          <v-title>Appears to return only list of students where attendance is due</v-title>
          <div style="max-width:100%;overflow:;padding:20px;">
            <pre>
              {{ recentlySubmitted.length }}
            </pre>
          </div>
        </v-col>
      </v-row> -->

    <!-- END DEV OUPUT   -->
   
    <!-- <span>Logged in as {{ user.firstname }}</span>   -->
    <!-- <div style="display:">
      <small> 
      <b>
        Day Moment MM/DD/YYYY formated : 
      </b>
        {{ fakeNowDay }}
      </small>
      <br>
      <small>
        <b>
          Date ISO formatted :
        </b>
        {{ fakeDayISO }}
      </small>
    </div> -->


    <!-- {{updateAlertRead}} -->

    <!-- <v-row no-gutters>
      <v-col md12>
        <h2 class="mb-3 font-weight-medium" style="color:#565656;border-bottom:1px solid rgb(169 165 165);">
          Overview
        </h2>
      </v-col>
      <v-col md1 style="text-align:end;">
        <h3 class="grey--text" style="color:#565656;border-bottom: 1px solid rgb(169 165 165);margin-top:20px;margin-top: 8px;">
          {{ new Date().toLocaleDateString(locale, { weekday: 'long' }) }}, {{  new Date().toLocaleDateString(locale, { month: 'long' }) }} {{  new Date().getDate() }}
        </h3>
      </v-col>
    </v-row> -->
<!-- 
    <div style="margin-bottom:10px;">
      <h2 class="mb-8 font-weight-medium" style="color:#565656;border-bottom: 1px solid rgb(169 165 165);">
        Overview
      </h2>
      <h5 class="grey--text">{{ new Date().toLocaleDateString(locale, { weekday: 'long' }) }}, {{  new Date().toLocaleDateString(locale, { month: 'long' }) }} {{  new Date().getDate() }}</h5>
    </div> -->
    
    
 <!-- TOP STATS ROW-->
 <!-- <Stats /> -->
 <!-- <h2 class="" style="color:rgb(150, 150, 150);font-size:24px;font-weight: 400;">Overview</h2> -->


<!-- <v-layout row wrap style="margin-bottom: 5px;"> -->
  <v-row style="margin-bottom: 30px;margin-top:0px">
    <v-col cols="12" xs="12" sm="12" md="12" lg="6" xl="6" class="px-3">
      <v-card>
        <v-card
          class="mx-auto"
          max-width=""
        >
          <v-list-item two-line>
            <v-list-item-content>
              <v-list-item-title class="text-h5" style="color: #706c6c">
                Next class
              </v-list-item-title>
              <!-- <v-list-item-subtitle>{{ classesFromStore[0]['fieldData']['scheduleDate'] }}</v-list-item-subtitle> -->
            </v-list-item-content>
          </v-list-item>

          <v-card-text>
            <v-row align="center">
              <v-col
                class="text-h4"
                cols="3"
              >
                Acme Inc.
              </v-col>
              <v-col 
                cols="3"
                class="text-h4"
              >
                Group 8 
                <!-- <v-img
                  src="https://cdn.vuetifyjs.com/images/cards/sun.png"
                  alt="Sunny image"
                  width="92"
                ></v-img> -->
              </v-col>
            </v-row>
          </v-card-text>

          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-calendar</v-icon>
            </v-list-item-icon>
            <v-list-item-subtitle>{{ classesFromStore[0]['fieldData']['scheduleDate'] }}</v-list-item-subtitle>
          </v-list-item>

          <v-list-item>
            <v-list-item-icon>
              <v-icon>mdi-clock</v-icon>
            </v-list-item-icon>
            <v-list-item-subtitle>{{ classesFromStore[0]['fieldData']['startTime']}}</v-list-item-subtitle>
          </v-list-item>

          <v-divider></v-divider>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn text
            @click="attendanceForm(classesFromStore[0])">
              Go To Class
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-card>
    </v-col>
    <v-col cols="12" xs="12" sm="12" md="12" lg="6" xl="6" class="px-3">
      <v-card class="px-0">
        tbd
      </v-card>
    </v-col>
  </v-row>
<!-- </v-layout> -->

<!-- v1 WIDGETS -->
<v-row v-show="false" class="top-stats" 
    md12
    sm12
    xs12
    justify="space-between"
    style="margin-bottom:0px"   
  >
  <v-col lg="4" cols="12">
    <v-card color="rgb(253 247 154)" class="recent-widget dash-widget" elevation="1" max-height="100%">
      <v-row class="" style="align-items: center;" no-gutters>

        <v-col cols="10">
          <v-card-title style="margin-top:0px;margin-left:10px; font-size: 20px;color:;">
            <!-- <span v-if="notes.length === 0">Schedule Updates</span> -->
    
            <!-- <span v-else>{{ notes.length }} Schedule Updates</span> -->
            <!-- {{ getNotes.length }} -->
          </v-card-title>
          <v-card-subtitle v-if="getNotes.length === 0" style="margin-left:10px">
            <span v-if="getNotes.length === 1">Schedule Update</span>
            <span v-if="getNotes.length > 1"> 
                Schedule Updates
            </span>
            <span v-else>No Schedule Updates</span>   
          </v-card-subtitle>
          <v-card-subtitle v-else style="margin-left:10px">Schedule updates</v-card-subtitle>
        </v-col>
        <v-col pa-10 cols="2" 
          style="margin-top: 0px;
          border: 0px solid red;
          /* background-color: #205999; */
          color: white;border-radius: 4px 0px 0px 4px;"
        >
        <v-icon color="green" style="background-color: rgb(158 224 95);
          padding: 15px;
          border-radius: 50%;
          font-size: 34px;">
          mdi-calendar-month
        </v-icon> 
          <!-- {{ getNotes.length }} -->
          <!-- <v-avatar
          class="widgets-avatar"
          color="red"
          size="80"
          style="width: 100%; height: 100%;"
          >
            <v-icon color="white">mdi-bell-outline</v-icon> 
            <v-icon color="white">
              <span v-if="notes.length === 0">0</span>
              <span v-if="notes.length > 1">{{ notes.length }}</span>
            </v-icon> 
          </v-avatar>   -->
            <!-- <span v-if="notes.length === 0">0</span>
            <span v-if="notes.length > 1">{{ notes.length }}</span>                                  -->
        </v-col>
      </v-row>
    </v-card>
  </v-col>

  <v-col lg="4" cols="12">
      <v-card color="#fff" class="recent-widget dash-widget" elevation="5" max-height="100%"
      style="background-color: #b0daff">
      <v-row class="" no-gutters style="align-items: center;">
        <v-col cols="9">
          <v-card-title style="margin-top:0px;margin-left:10px; font-size: 20px;color:;">
            {{ getAllClassesToday.length }} 
          </v-card-title>
          <v-card-subtitle v-if="getAllClassesToday.length < 1" style="margin-left:10px">
            <!-- {{getAllClassesToday.length}} classes scheduled today -->
            <!-- Classes Today -->
            {{getAllClassesToday.length === 1 ? 'Class Today' : 'Classes Today'}}
          </v-card-subtitle>
        </v-col>
        <v-col pa-10 cols="3" 
            style="margin-top: 0px;
            line-height: 8;
            text-align: center;
            /* background-color: rgb(112 158 124); */
            color: white;
            border-radius: 4px 0px 0px 4px;"
        >
        <v-icon color="white" style="background-color: #3ca2fa;
          padding: 15px;
          border-radius: 50%;font-size:34px;">
          mdi-school</v-icon> 

            <!-- {{getAllClassesToday.length}}  -->
            <!-- <v-avatar
            class="widgets-avatar"
            color="blue"
            size="80"
            style="width: 100%; height: 100%;"
          >
            <v-icon color="white">mdi-calendar</v-icon> 
          </v-avatar>                                    -->
        </v-col>
      </v-row>
    </v-card>

  
    <!-- <v-card color="#fff" class="recent-widget" elevation="1" height="100%">
      <v-list-item>  
        <v-list-item-content>
          <v-list-item-title style="font-size:24px">
            <v-list-item-avatar color="red" size="50">
          <v-icon class="" v-text="'mdi-bell-outline'" style="color:white"></v-icon>
        </v-list-item-avatar>{{ notes.length }}</v-list-item-title>
        <br />
        <v-list-item-subtitle v-text="'Class Updates'" style="font-size:16px;margin-left:0px"></v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
    </v-card> -->
  </v-col>

  <v-col lg="4" cols="12">
      <v-card color="#fff" class="recent-widget dash-widget" elevation="2" max-height="100%"
      style="background-color: rgb(70 184 196);">
      <v-row class="" no-gutters>
        
        <v-col cols="10">
          <v-card-title style="margin-top:2px;margin-left:10px">
            {{ classesWithIncompleteAttendance.length }}
          
          </v-card-title>
          <v-card-subtitle style="margin-left:10px">Classes with attendance due</v-card-subtitle>
        </v-col>

        <v-col pa-10 cols="2" 
            style="margin-top: 0px;
            line-height: 3;
            font-size: 29px;
            text-align: center;
            border: 0px solid red;
            background-color: #38b4c1f2;
            color: white;
            border-radius: 4px 0px 0px 4px;"
          >
        <v-icon color="white">mdi-check</v-icon> 

            <!-- {{ classesWithIncompleteAttendance.length }} -->
            <!-- <v-avatar
            class="widgets-avatar"
            color="green"
            size="50"
            style="margin:10px;margin-left:15px">
            <v-icon color="white">mdi-form-select</v-icon> 
          </v-avatar>                                    -->
        </v-col>


      </v-row>
    </v-card>

    <!-- <v-card color="#fff" class="recent-widget" elevation="1" height="100%">
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title style="font-size:24px">
            <v-list-item-avatar color="orange" size="50">
          <v-icon class="" v-text="'mdi-form-select'" style="color:white"></v-icon>
        </v-list-item-avatar>{{ classesWithIncompleteAttendance.length }}</v-list-item-title>
        <br />
        <v-list-item-subtitle v-text="'Classes with attendance due'" style="font-size:16px;margin-left:30px"></v-list-item-subtitle>        
        </v-list-item-content>
      </v-list-item>
    </v-card> -->
  </v-col>

  <!-- <v-col md="2">
      <v-card style="height=100%" elevation="1">
        <v-card-title style="justify-content:center">
          <span>
            <h3 text-align="center">{{ new Date().toLocaleDateString(locale, { weekday: 'long' }) }}</h3>
          </span>
        </v-card-title>
        <v-card-title style="justify-content:center">
          <span>
            <v-avatar
              class="widgets-avatar"
              color="blue"
              size="80"
            >
              <span class="white--text text-h2">{{  new Date().getDate() }}</span>
            </v-avatar>   
          </span>
        </v-card-title>
        <v-card-title style="justify-content:center">
          <span>
            <h3 text-align="center">{{ new Date().toLocaleDateString(locale, { month: 'long' }) }}</h3>
          </span>
        </v-card-title>
      </v-card>
  </v-col> -->
  
</v-row>
<!-- END TOP STATS ROWS -->


    <!-- DUE LIST -->
    <!-- <v-row no-gutters style="margin-bottom: 20px;
      border-bottom: 1px solid lightgray;
      /* background-color: rgb(0 112 209); */
      padding: 14px;
      border-radius: 0px 0px 0px 0px;
    
      /* box-shadow: rgb(196 198 200) 0px 0px 6px -2px; */">
      <h2 class="mb-1 font-weight-medium" 
        style="font-size: 24px;
   
        /* color: rgb(234 240 247); */
        color: rgba(131, 131, 131, 0.93);
        letter-spacing: 0.09px;">
        Attendance Due
      </h2>
    </v-row> -->



    <v-row no-gutters>
        <h2 class="mb-1 font-weight-medium" style="color: rgb(131 131 131 / 93%);margin-right: 20px;">
          Attendance Due <small>(options)</small>
        </h2>
        <span style="width: 20px;
          height: 20px;
          background-color: #ff9d3c;
          border-radius: 50%;
          justify-content: flex-start;
          align-items: center;
          text-align: center;
          /* color: aliceblue; */
          align-content: center;
          align-items: baseline;
          line-height: -1%;
          /* position: absolute; */
          /* top: 0%; */
          vertical-align: middle;
          font-size: 12px;
          /* line-height: 100%; */
          align-items: start;
          vertical-align: middle;
          /* display: inline-block; */
          margin-left: 15px;
          /* word-break: break-word; */
          /* white-space: normal; */
          /* border: 1px solid grey; */
          color: #fff;
          margin-top: 7px;">
          {{ classesWithIncompleteAttendance.length }}
        </span>
    </v-row>

    <!-- {{ classesWithIncompleteAttendance }} -->

    <!-- ATTENDANCE UP-TO-DATE -->
    <v-row no-gutters v-show="classesWithIncompleteAttendance.length < 1" 
      style="text-align: center;margin-bottom: 30px;">
      <v-col style="padding: 20px;background-color: #f0f0f0;">
        <v-icon style="padding: 10px;
          background-color: rgb(224 224 224);
          border-radius: 8px;
          font-size: 38px;
          margin-bottom: 10px;
          color: #7070708c;">mdi-check</v-icon>

        <div style="color: rgb(144 141 141);
          font-size: 24px;">
          Attendance is up-to-date
        </div>
      </v-col>  
    </v-row>

    <template v-if="classesWithIncompleteAttendance.length > 0" 
      style="margin-bottom: 150px !important;border: 1px solid red;"
    >
    <!-- <v-hover v-slot="{ hover }"> -->
      <v-card v-for="(item,index) in classesWithIncompleteAttendance" 
      :key="index"
      :elevation="hover ? 6 : 1"
      :class="{ 'on-hover': hover }"
      @click="attendanceForm(item)" 
      style="margin-bottom: 20px !important;
      border-left: 5px solid #41c14d;">
        <v-layout class="pa-3 project" style="margin-top: 4px">
          <v-flex xs3 sm4 md2>
            <div class="caption grey--text">Date</div>
            <div>
              <!-- {{ formatDate(item['fieldData']['scheduleDate'])}} -->
              <ul style="list-style:none;padding:0px">
                <li style="list-style:none;">{{ formatDate(item['fieldData']['scheduleDate'])[0] }}, {{ formatDate(item['fieldData']['scheduleDate'])[1] }}</li>
                <!-- <li style="list-style:none">{{ formatDate(item['fieldData']['scheduleDate'])[1] }}</li> -->
                <li style="list-style:none;">{{ formatDate(item['fieldData']['scheduleDate'])[2] }}</li>
              </ul>
            
            </div>
          </v-flex>

          <v-flex xs3 sm4 md2>
            <div class="caption grey--text">Client</div>
            <!-- <div>Client name</div> -->
            <!-- {{ item  }} -->
            <span v-if="item['fieldData']['class_reg_students_CLIENTS::clientName']"> {{ item['fieldData']['class_reg_students_CLIENTS::clientName'] }}</span>
            <span v-else>N/A</span>
          </v-flex>

          <v-flex xs7 md6>
            <div class="caption grey--text">Student/Group</div>
            <div>
              <span v-if="item['portalData']['class_REGISTRATIONS'].length === 1">   
                {{ item['portalData']['class_REGISTRATIONS'][0]['class_reg_STUDENTS::firstName'] }} {{ item['portalData']['class_REGISTRATIONS'][0]['class_reg_STUDENTS::lastName'] }}
              </span> 
              <span v-if="!item.groupNo && item['portalData']['class_REGISTRATIONS'].length !== 1">
                <!-- No data - please contact course coordinator -->
                {{ item['fieldData']['SCHEDULES::groupName'] }}
              </span>
              <!-- <span v-if="item.groupNo">
                - Group {{ item.groupNo }}
              </span> -->
            </div>                     
          </v-flex>

          <v-flex xs2 sm4 md2 style="justify-content: center;
            text-align: right;
            align-items: center;
            margin-top: 10px;"
          >
            <v-btn
              @click="attendanceForm(item)"
              class="mx-0"
              fab
              small
              color="rgb(243 174 29)"
            >
              <v-icon style="color:white">
                mdi-chevron-right
              </v-icon>
            </v-btn>
          </v-flex>
        </v-layout>
        <!-- <v-divider></v-divider> -->
      </v-card>
    <!-- </v-hover> -->

    </template>


<!-- TEST FROM WIREFRAME -->
    <!-- <v-row>
          <v-col cols="12">
            <v-card>
              <v-subheader>Attendance Due</v-subheader>
              <v-list two-line>
                <template  v-for="(item,index) in classesWithIncompleteAttendance">
                  <v-list-item
                    v-bind:key="index"
                  >
                    <v-list-item-avatar color="grey darken-1">
                    </v-list-item-avatar> 
                    <v-list-item-content>
                      <v-list-item-title>{{ item.name }}</v-list-item-title>

                      <v-list-item-subtitle>
                        {{ item.displayDate }}
                      </v-list-item-subtitle>
                    </v-list-item-content>
                  </v-list-item>

                  <v-divider
                    v-if="index !== totalAttendanceDue -1"
                    :key="index"
                    inset
                  ></v-divider>
                </template>
              </v-list>
            </v-card>
          </v-col>
        </v-row> -->

<!-- END TEST WRIREFRAME -->

    <!-- <v-row no-gutters style="
      background-color: rgb(255 255 255);
      padding: 18px;
      border-radius: 7px;
      box-shadow: rgb(196 198 200) 0px 0px 16px -2px;
      margin-bottom: -10px;
      border-bottom-right-radius: 0px;
      border-bottom-left-radius: 0px;">
        <h2 class="mb-1 font-weight-medium" style="color: rgb(131 131 131 / 93%);">Attendance Due</h2>
    </v-row>

    <v-row no-gutters v-if="classesWithIncompleteAttendance.length < 1" style="text-align: center;
      margin-bottom: 30px;">
      <v-col style="padding: 20px;background-color: #f0f0f0;">
        <div style="color: rgb(143 140 140);font-size: 20px;">
          Attendance is up-to-date
        </div>
      </v-col>  
    </v-row>
      
    <template v-if="classesWithIncompleteAttendance.length > 0" style="margin-bottom: 50px;border: 1px solid red;">
      <v-simple-table class="dash-table" elevation="3">
        <template v-slot:default>
          <thead>
            <tr>
              <th class="text-left" style="color:#000">
                Class Date
              </th>
              <th class="text-left" style="color:#000">
                Student/Group
              </th>

              <th class="text-left" style="color:#000; text-align:center !important">
                Attendance
              </th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="(item,index) in classesWithIncompleteAttendance"
              :key="index"
            >
              <td>{{ formatDate(item.displayDate) }}</td>
              <td>{{ item.name }}</td>

              <td align="center">
                <v-btn
                  @click="attendanceForm(item)"
                  class="mx-0"
                  fab
                  dark
                  small
                  color="#faae19"
                >
                  <v-icon dark >
                    mdi-pencil
                  </v-icon>
                </v-btn>
              </td>
            </tr>
          </tbody>
        </template>
      </v-simple-table>
    </template> -->
            
            <!-- <v-badge v-if="item === 'Schedule Updates' && notes.length"
              color="blue"
              :v-bind="notes.length"
              :content="notes.length"
              inline
            >
            </v-badge> 
            <v-badge v-if="item === 'Attendance Due' && classesWithIncompleteAttendance.length > 0"
              color="red"
              :content="classesWithIncompleteAttendance.length"
              inline
            >
            </v-badge>    
              {{ item }}
            </v-tab>
          </v-tabs>
        </template>
      </v-toolbar>

      <v-tabs-items v-model="tab">
        <v-tab-item
          v-for="(item, index) in items"
          :key="index"
        >
          <v-card elevation="2">
            <v-card-text v-if="item === 'Schedule Updates' && notes.length"> 
              <v-simple-table>
                <template v-slot:default>
                  <thead>
                    <tr>
                      <th class="text-left">
                        Class Date
                      </th>
                      <th class="text-left">
                        Client / Student
                      </th>
                      <th class="text-left">
                        Details
                      </th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr
                      v-for="(item, index) in notes"
                      :key="index"
                    >
                      <td>{{ item.displayDate }}</td>
                      <td>{{ item.name }} <span v-if="!item.isPrivate"> - Group  {{ item.groupNo }}</span></td>
                      <td>{{ item.noteToTeacher }}</td>
                    </tr>
                  </tbody>
                </template>
              </v-simple-table>
            </v-card-text>

            <v-card-text v-if="item === 'Schedule Updates' && !notes.length">
              No new updates since last login.
            </v-card-text>
            
            <v-card-text v-if="item === 'Attendance Due' && classesWithIncompleteAttendance.length > 0">  
              <p>{{ classesWithIncompleteAttendance.length }} attendance records currently due for this period.</p>
              <v-simple-table>
                <template v-slot:default>
                  <thead>
                    <tr>
                      <th class="text-left">
                        Class Date
                      </th>
                      <th class="text-left">
                        Student / Group
                      </th>
                      <th class="text-left">Attendance</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr
                      v-for="item in getAllClasses"
                      :key="item.name"
                    >
                      <td>{{ item.displayDate }}</td>
                      <td v-if="!item.isPrivate">{{ item.name }} - Grp: {{ item.groupNo }}</td>
                      <td v-else>{{ item.name }}</td>

                      <td>
                        <v-btn
                          @click="attendanceForm(item)"
                          class="mx-0"
                          fab
                          dark
                          small
                          color="cyan"
                        >
                          <v-icon dark>
                            mdi-pencil
                          </v-icon>
                        </v-btn>
                      </td>
                    </tr>
                  </tbody>
                </template>
              </v-simple-table>
            </v-card-text>  
            <v-card-text else>Attendance is up to date for this period</v-card-text>
            
            <v-card-text v-if="item === 'Recently Submitted' && recentlySubmitted.length">  
              <v-simple-table>
                <template v-slot:default>
                  <thead>
                    <tr>
                      <th class="text-left">
                        Class Date
                      </th>
                      <th class="text-left">
                        Student
                      </th>
                      <th class="text-left">
                        Attendance Submitted
                      </th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr
                      v-for="item in recentlySubmitted"
                      :key="item.fname"
                    >
                      <td>{{ item.classDate }}</td>
                      <td>{{ item.fname }}  {{item.lname}}</td>
                      <td>  
                        <v-icon style="color:green" v-if="item.attendanceSubmitted === true">
                          mdi-checkbox-marked-circle-outline
                         
                        </v-icon>                 
                      </td>
                    </tr>
                  </tbody>
                </template>
              </v-simple-table>
            </v-card-text>
            <v-card-text v-if="item === 'Recently Submitted' && !recentlySubmitted.length">
              No attendance records to display
            </v-card-text>
           </v-card>
        </v-tab-item>
      </v-tabs-items>
    </v-card> --> 

    <!-- 2nd Row -->
    <!-- <v-layout row wrap>
      <v-row md12
        sm12
        xs12
        justify=""
        style=""
      >

        <v-col lg=4>  
          <v-flex md12 sm12 xs12>
            <v-card color="#fff" class="recent-widget" elevation="1" height="100%">
              <v-card-title class="px-3">
                    <v-avatar
                      class="widgets-avatar"
                      color="green"
                      size="50"
                      style="margin-right: 10px;margin-left:10px;"
                    >
                    <v-icon color="white">mdi-clipboard-outline</v-icon>
                  </v-avatar>                                   
                  Upcoming Classes
              </v-card-title>
              <span v-if="this.recentlySubmitted.length">
                <v-card-text v-if="true" class="text-wrap">
                  You have 4 classes scheduled today
                </v-card-text>
                <v-card-text v-else-if="attendanceUpToDate">
                  You have no classes today
                </v-card-text>
              </span>
            </v-card>
          </v-flex>
        </v-col>

        <v-col>  
          <v-flex md12 sm12 xs12>
            <v-card color="#e1e6e7f2" class="recent-widget">
              <v-card-title class="px-3">
                    <v-avatar
                      class="widgets-avatar"
                      color="orange"
                      size="50"
                      style="margin-right: 10px;margin-left:10px;"
                    >
                    <span class="white--text text-h4">5</span>
                  </v-avatar>                                   
                  Recently Sub
              </v-card-title>
             
                <v-card-text v-if="!attendanceUpToDate" class="text-wrap">
                
                  Some attendance records have yet to be submitted for this period. 
                  Please see Attendance Due below for information.
                  {{ someComputed }}
                </v-card-text>
                <v-card-text v-else-if="attendanceUpToDate">
                  All attendance up to date.
                </v-card-text>
         
            </v-card>
          </v-flex>
        </v-col>

        
      </v-row>
    </v-layout> -->

  <!-- <v-container class="grey lighten-5" fluid> -->
    <!-- <v-row md12
        sm12
        xs12
        justify="space-between">
      <v-col
        style=""
      >
        <v-card
          class="pa-2 grad dash-widget"
          outlined
          tile
          elevation="1"
        >
        <v-list-item>
         
          <v-list-item-content>
            <v-list-item-title style="font-size:24px">
               <v-list-item-avatar color="red">
            <v-icon class="" v-text="'mdi-form-select'" style="color:white"></v-icon>
          </v-list-item-avatar>{{ classesWithIncompleteAttendance.length }}</v-list-item-title>
           <br />
          <v-list-item-subtitle v-text="'Class Attendance Due'" style="font-size:16px;margin-left:30px"></v-list-item-subtitle>
           
           
          </v-list-item-content>
        </v-list-item>

          <v-card-title class="px-0">
            <v-avatar
              class="widgets-avatar"
              color="red"
              size="50"
              style="margin-right: 10px;margin-left:10px;"
            > 
            <v-icon color="white">mdi-form-select</v-icon>
            </v-avatar>       
            {{ classesWithIncompleteAttendance.length }} Class Attendance Due
          </v-card-title>

          <v-card-text v-if="true" class="text-wrap">
            Please see details section below for information.
          </v-card-text>
          <v-card-text v-else-if="false">
            All attendance up to date.
          </v-card-text>
        </v-card>
      </v-col>

      <v-col>
        <v-card
          class="pa-2 dash-widget"
          outlined
          tile
          elevation="1"
        >
          <v-card-title class="px-0">
            <v-avatar
              class="widgets-avatar widget-orange"
              color="orange"
              size="50"
              style="margin-right: 10px;margin-left:10px;"
            ><v-icon color="white">mdi-calendar</v-icon>
            </v-avatar>                                   
              {{ totalClasses.length }} Classes in this period 2
          </v-card-title>
          <v-card-text>
          {{ getAllClasses.length }} Classes require attendance
          </v-card-text>
        </v-card>
      </v-col>


      <v-col>
        <v-card
          class="pa-2 grad dash-widget"
          outlined
          tile
          elevation="1"
        >
          <v-card-title class="px-0">
            <v-avatar
              class="widgets-avatar"
              color="orange"
              size="50"
              style="margin-right: 10px;margin-left:10px;"
            >
              <span class="white--text text-h3">{{ totalClasses.length }}</span>
            </v-avatar>                                   
              Classes in this period 3
          </v-card-title>
          <v-card-text>
          {{ getAllClasses.length }} Classes require attendance
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
     -->
   <!-- <v-row>
      <v-col
        v-for="n in 3"
        :key="n"
        cols="12"
        sm="4"
      >
        <v-card
          class="pa-2 grad"
          outlined
          tile
        >
          <v-card-title class="px-0">
            <v-avatar
              class="widgets-avatar"
              color="orange"
              size="50"
              style="margin-right: 10px;margin-left:10px;"
            >
              <span class="white--text text-h3">{{ totalClasses.length }}</span>
            </v-avatar>                                   
              Classes in this period
          </v-card-title>
          <v-text>
          <small>{{ getAllClasses.length }} Classes require attendance</small>
          </v-text>
        </v-card>
      </v-col>
    </v-row> -->
  <!-- </v-container> -->
 <!-- <v-layout row wrap>  -->

    <!-- <v-row md12>
      <v-col cols="1" lg="12">
        <v-card> 
          <v-card-title class="px-3">
            Dates Widget
          </v-card-title>
          <v-card-text>          
            <label for="now">Today's date by month: </label> {{ this.fakeNowMonth }}
            <br>
            <label for="date-range">Date Range for classes: {{ this.dateRange }} </label>
            <br>
            <label for="yday">
              Yesterday = date up to which to check existing attendance : {{ this .yesterday }}
            </label>
            <br>
            <label for="two-weeks-ago">Two weeks and day ago : </label> {{ this.twoWeeksAndDayAgo }}
          </v-card-text>
        </v-card> 
      </v-col>
    </v-row> -->

 <!-- </v-layout> -->

    <!-- V-DATE-PICKER -->
    <!-- <v-row style="display:">
      <v-col
        cols="12"
        sm="6"
      >
        <v-date-picker
          v-model="dates"
          color="green lighten-1"
          range
        ></v-date-picker>
      </v-col>
      <v-col
        cols="12"
        sm="6"
      >
        <v-text-field
          v-model="dateRangeText"
          label="Date range"
          prepend-icon="mdi-calendar"
          readonly
        ></v-text-field>
        model: {{ dates }}
        <v-btn @click="getTwoWeekAttendance">vlick</v-btn>
      </v-col>
    </v-row>  -->


    <!-- <upcoming-classes :key="rerenderWidgets" :notesArr="notes"/>    -->

    <!-- <v-layout class="" row wrap>
      <v-flex md6 xs12 >
        <v-card light elevation="" >
          <monthly-sales /> 
           {{ notes }}
          <Notes v-if="notes.length" :notesArr="notes"/>
        </v-card>
      </v-flex>

      <v-flex md6 xs12>
        <v-card light elevation="4">
          <order-forecast />
        </v-card>
      </v-flex> 
    </v-layout> -->


    <!-- <v-layout class="" row wrap>
      <v-flex md6 xs12>
        <v-card light elevation="4">
          <product-analysis />
        </v-card>
      </v-flex>
      <v-flex md6 xs12 >
        <v-card light elevation="4">
          <browser-usage></browser-usage>
        </v-card>
      </v-flex>
    </v-layout> -->

      <!-- <v-snackbar v-model="snackbar.visible" auto-height :color="snackbar.color" :multi-line="snackbar.mode === 'multi-line'" :timeout="snackbar.timeout" :top="snackbar.position === 'top'">
        <v-layout align-center pr-4>
          <v-icon class="pr-3" dark large>{{ snackbar.icon }}</v-icon>
          <v-layout column>
            <div>
              <strong>{{ snackbar.title }}</strong>
            </div>
            <div>{{ snackbar.text }}</div>
          </v-layout>
        </v-layout>
        <v-btn v-if="snackbar.timeout === 0" icon @click="snackbar.visible = false">
          <v-icon>clear</v-icon>
        </v-btn>
      </v-snackbar> -->

  </v-container>
</template>

<script lang="ts">
import computed from 'vue'
import Stats from "@/components/dashboard/topStats.vue";
// import MonthlySales from "@/components/dashboard/MonthlySales";
// import Notes from "@/components/dashboard/Notes.vue";
// import OrderForecast from "@/components/dashboard/OrderForecast";
// import BarChart from "@/components/dashboard/Bar";
// import BrowserUsage from "@/components/dashboard/BrowserUsage";
import { Component, Prop, Watch } from "vue-property-decorator";
import UpcomingClasses from "@/components/dashboard/UpcomingClasses.vue";
import { classesModule } from "@/store/modules/classes";
import { attendanceModule } from "@/store/modules/attendance";
import { userModule } from '@/store/modules/user';
import router from '@/router';
import moment from 'moment';
import DatePicker from 'vue2-datepicker'
import { getDefaultPagination, getPagination } from '@/utils/store-util';

import axios from 'axios'

import Vue from "vue";
import { at } from "lodash";

@Component({
  name: "Dashboard",
  // Customize these for teacher specific stats
  components: {
    // BarChart
    // TODO: CUSTOM WIDGETS
    UpcomingClasses,
    // Notes,
    DatePicker, // TODO
    Stats,
  }
})

export default class Dashboard extends Vue {
  public currentTime = new Date().toLocaleString()
  public viewingAsAdmin = false
  public classesFromStore
  public missingDataAlert = ''
  private viewingAsFullName = '';
  public numClasses: number; // FIX: not appearing in template
  // private changeNum
  public classes: Array<object> = []
  public  monthlyStats
  private widgetsVisible
  private rerenderWidgets = 0
  private dateRange
  private fakeNowMonth
  private fakeNowDay
  private fakeDayISO
  private yesterday
  private twoWeeksAndDayAgo
  private dates = ['2020-12-02', '2020-12-04']
  private existingRecords: Array<object> = []
  private checkAttendanceRequests = 0
  private numAttendanceRecords
  private records 
  private numStudents
  // private currentStudents: Array<TODO> = []
  private currentStudents
  private missingRecords: Array<object> = []
  // private attendanceUpToDate: boolean
  private attendanceAlert
  private text = "Some dynamic messgage here"
  private upcomingClasses
  private notesArr: Array<TODO>
  private showUpdateAlert = true
  private lastSubmittedClass
  private numTest = 0
  // private allClasses
  private lastUpdated
  private API_msg 
  private allClasses2

  private submitAlertToggle = true
  private updateAlerts = []

  // TABS  
  private currentTab = 0
  private tabs = [
    { title: 'Overview', icon: 'mdi-clipboard-text'}, 
    { title: 'Schedule Updates', icon: 'mdi-update' },  
    { title: 'Attendance Due', icon: 'mdi-account-check'}, 
    // { title: 'My Schedules', icon: 'mdi-calendar-month'}, 
  ]

  private  projects = [
        { title: 'Design a new website', person: 'The Net Ninja', due: '1st Jan 2019', status: 'ongoing', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!'},
        { title: 'Code up the homepage', person: 'Chun Li', due: '10th Jan 2019', status: 'complete', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!'},
        { title: 'Design video thumbnails', person: 'Ryu', due: '20th Dec 2018', status: 'complete', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!'},
        { title: 'Create a community forum', person: 'Gouken', due: '20th Oct 2018', status: 'overdue', content: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Sunt consequuntur eos eligendi illum minima adipisci deleniti, dicta mollitia enim explicabo fugiat quidem ducimus praesentium voluptates porro molestias non sequi animi!'},
  ]

  private cards = ['Today', 'Yesterday']
  private links = [
        ['mdi-inbox-arrow-down', 'Inbox'],
        ['mdi-send', 'Send'],
        ['mdi-delete', 'Trash'],
        ['mdi-alert-octagon', 'Spam'],
      ]

  /** Pagination */
  private attendanceDuePageSize = 5
  private attendancePage = 1
  private attendanceDueListCount = 0
	private attendanceDueHistoryList = []  
  private updateItems = []  
  private schedulePagination = {}

  data () {
      return {
        tab: '',
        items: [
          'Schedule Updates', 'Attendance Due', 'Recently Submitted','Upcoming Classes', 
        ],
        page:1, // Pagination TODO
        pageCount: 0,
        itemsPerPage: 3,
        updatesHeaders: [
          { text: 'Date', align: 'left', filterable: false, value: 'scheduleDate' },
          { text: 'Class', value: 'classesNumber' },
          { text: 'Note', value: 'teacherNotes' },
          { text: 'Action', value: '__pk_Classes' },
        ],
      }

  }
      

  @Watch('submitAlertToggle')
  onPropertyChanged(value: boolean, oldValue: boolean) {
    console.log('new valuez:', value + ' ' + 'Old Value:' + oldValue)
    // alert('Check console for alert value change...')
    sessionStorage.setItem('updatedClassAttendance', '')
    // return value
  }

  async mounted() {

    // Get notes for table
    this.updateItems = classesModule.getNotes.map(n => n['fieldData']).map((item) => {
      return {
        details: {},
        ...item
      }

    })
    // console.log('Beer : ', this.updateItems)


    // axios.get('https://api.punkapi.com/v2/beers?page=1&per_page=50')
    //     .then(response => {
    //       this.updateItems = response.data.map((item) => {
    //           return {
    //             details: {},
    //             ...item
    //           }
    //       })
    //  })
    // Check if a submitted class has suceeded with full attendance 
    // If registration === number of success responses (with recordId) 
    // Then add the classId in local storage array
    // Compare the classes in the attendance due results
    // If it is there remove it

    this.fakeNowDay = moment().format('01/04/2021')
    this.fakeDayISO = moment('01/04/2021').toISOString()

    const updateAlertStatus = await localStorage.getItem('Update Read')
    // alert(`${updateAlertStatus}`)
    if(updateAlertStatus === 'true') { this.showUpdateAlert = false }
    
    const lastSub = sessionStorage.getItem('submittedClass')
    if(lastSub !== '') {
      // alert(`last submitted -> ${lastSub}`) 
      console.log(`Dash: last submitted record -> ${lastSub}`)
      sessionStorage.removeItem('submittedClass')
    }
  }

  async attendanceForm(e) {

    // this is object - must get length
    console.log('cls -> ', e)
    console.log('class from dash -> ', typeof(e['portalData']['class_REGISTRATIONS']))

    const modCheck = classesModule.checkForRecordModifedinFM(e)
    let classEvent = {}
    let color

    // if(e['fieldData']['teacherNotes'] !== "") {
    //   color = 'black'
    // } 

    // Get name of single student  
    if(e['portalData']['class_REGISTRATIONS'].length === 1) {
      classEvent.name = e['portalData']['class_REGISTRATIONS'][0]['class_reg_STUDENTS::firstName'] + ' ' + e['portalData']['class_REGISTRATIONS'][0]['class_reg_STUDENTS::lastName']
      classEvent.groupNo = null
      console.log('we go -> ', classEvent)
    } else {
      classEvent.name = 'XYZ Comp'
      classEvent.groupNo = e['fieldData']['groupNo'] || "GRP007" 
    }

    classEvent = { ...classEvent,
        "color": color,  
        "classID": e['fieldData']['__pk_Classes'], 
        "type": e['fieldData']['type'] || 'Data Missing' , 
        "date": e['fieldData']['scheduleDate'], 
        "start": e['fieldData']['startTime'], 
        "end": e['fieldData']['endTime'], 
        "noStudents": e['portalData']['class_REGISTRATIONS'].length, 
        "registrations": e['portalData']['class_REGISTRATIONS'] , 
        "noteToTeacher": e['fieldData']['teacherNotes'], 
        "details": [ { "note": "no notes here" }, { "msg": "hello attendance msg" } ] 
      }

    console.log('class obj ready for att -> ', classEvent)


    sessionStorage.setItem('routeFrom', 'dash')
    classesModule.setIndexForCurrentClass(e)
    console.log('indx of event in calendar', e)

    const fullData = await classesModule.getFullClassData(e['fieldData']['__pk_Classes']) 

    console.log('Now in dash -> ', fullData)

    const selectedClassFull = JSON.stringify(fullData)

    sessionStorage.setItem('selectedClassFull', selectedClassFull)

    // Must set the selected class format to the same as from calendar card 


    await sessionStorage.setItem('selectedClass', JSON.stringify(classEvent))
    this.$router.push({ name: 'attendance'}) 
    // this.$router.push({ name: 'attendance', query: { event: e }})
  }

 

  // private snackbar = {
  //   color: "success",
  //   icon: "mdi-check-circle",
  //   mode: "multi-line",
  //   position: "top",
  //   timeout: 7500,
  //   title: "Success",
  //   text: "You are signed in!",
  //   visible: true
  // }

  get updatedEventForAlert () {
    return classesModule.getSingleClass
    // const ula = JSON.parse(sessionStorage.getItem('updatedClassAttendance'))
    // this.updateAlerts.push(ula)
    // if(ula === null || ula === undefined || ula === '') {
    //   console.log('here ', ula)
    //   return ula
    // } else {
    //     return ula
    // }
  }

  get nextClass() {
    let next 
    classesModule.getAllClasses().then(res => {
      next = res
    })
    return next
  }

  get userFirstName() {
    const fName = this.user.teacher_name.split(" ") 
    return fName[0]
  }

  get user() {
    const signedInUser = JSON.parse(userModule.userFromStorage);
    return signedInUser
  }

  // Move to backend auth
  get isAdmin() {
    const isAdmin = sessionStorage.getItem('isAdmin')
    if(isAdmin === 'true') {
      return true
    }
    return false
  }

  // get user() {
  //   // return sessionStorage.getItem('fm-user')
  //   return userModule.signedInUser;
  // }
  get getAllClassesToday(){   
    // "start": "2021-01-04 11:30:00", -> format in class object
    // Set today = today's date in production to get all classes on today's schedule
    // const today = moment('2021-01-06').format('YYYY-MM-DD')
    const today = moment('2021-01-05').format('YYYY-MM-DD')
    this.fakeNowDay = today

    const classes = classesModule.getClasses
    const classesToday = classes.filter(e => {
      const classDate = moment(e.start).format('YYYY-MM-DD')
      console.log('a class -> ', classDate)
      return today == classDate 
    })
    return classesToday
  }

  // get getAllClasses() {
  //   this.allClasses = classesModule.getClasses
  //   const classesWithAttDue = this.allClasses.filter((c,i) => {
  //     console.log('class ', c)
  //     if(c.isAttendanceComplete === false) { return c }   
  //     const foundClasses = c['students'].filter((s) => {
  //       if(s.attendanceSubmitted === false ) {
  //         return c
  //       }
  //     })
  //   console.log('Classes with att due -> ', classesWithAttDue)
  //   return classesWithAttDue
  // }

  // get currentStudentList() {
  //   return this.currentStudents
  // }
   

  // constructor() {
  //  super()
  // }

  // data: () => ({
  //     dates: ['2019-09-10', '2019-09-20'],
  //   })
  //   computed: {
  //     dateRangeText () {
  //       return this.dates.join(' ~ ')
  //     }
  //   }

  // TODO: fix the bug with API for finding previously submitted attendance records
  // Needed to build out an informative dash

  get someComputed() { 
    return 'this text is computed again'
  }  

  formatDate(d) {

    
    const formatted = moment(d).format("ddd, Do MMM, gggg")
    const splitD = formatted.split(',')
    console.log('D fromat ', splitD)

    // extract individual date elements 

    return splitD
  }

  get partials() {
    return classesModule.partialCompleteAttendance
  }

  // SET Partial completed class 
  classesWithPartialAttendance() {
      alert('[dash]classesWithPartialAttendance')
      const cParse  = JSON.parse(JSON.stringify(this.classes))
      console.log('ITEMS -> ', cParse)
      const res = this.classes.filter(c => {
        const num1 = c['portalData']['class_REGISTRATIONS'].length()
        alert(`${num1}`)
        const sum = c['portalData']['class_REGISTRATIONS'].length() - c['portalData']['class_ATTENDANCES'].length() !== c['portalData']['class_REGISTRATIONS'].length()
        console.log('partial att -> ', sum)
        return c
      })
      return res
  }

  setViewingAsTeacher() {
      const selectedTeacher = sessionStorage.getItem('viewAsTeacher')
      const parsedT = JSON.parse(selectedTeacher)
      const teacherFullName =  parsedT['firstname'] + ' ' +  parsedT['lastname'] 
      console.log('[setViewingAsTeacher] ->', teacherFullName)
      this.viewingAsFullName = teacherFullName
      return parsedT
  }
  
  async adminViewing() {
    const routeFrom = await sessionStorage.getItem('routeFrom') 
    if(routeFrom === 'admin') {
      alert('viewing as admin...')
      this.viewingAsAdmin = true
      return true
      // make a new FM call for specific teacher data 
    } else {
      this.viewingAsAdmin === false
      return false
      // check the store direct for classes 
    }
  }

  beforeCreate() {
    if (sessionStorage.getItem('fm-err')) {
      alert('go to 404...')
      this.$router.push('/fm-err');
    }
  }

  async created() {

    setInterval(() => {
      // call classes.ts or fm-api.ts direct from here 
    }, 5000)

    setInterval(() => {
      this.currentTime = new Date().toLocaleString()
    }, 1000)
    // alert('created')
    // Set up dates and date range for app
    const fakeNowDay = moment().format('MM/DD/YYYY')
    console.log('[created] today date ... ', fakeNowDay)

    // check from route 
    if(this.adminViewing()) {
      // alert('You are viewing as admin...')
      const teacherInView = this.setViewingAsTeacher()
      // alert(`Viewing -> ${teacherInView['firstname']} as Admin`)
    }


      this.classesFromStore = await classesModule.getAllClasses()
      console.log('CFS', this.classesFromStore)

      const newNotes = classesModule.getNotes.map(n => n['fieldData'])
      this.schedulePagination = getPagination(newNotes) 

      const signedInAsAdmin = sessionStorage.getItem('isAdmin') 

      const pAdmin = JSON.parse(signedInAsAdmin)
      console.log('ADMIN -> ', pAdmin)

      // Avoid repeated API calls if classes already exist in app
      // TODO: schedule updates?? 
      console.log('Class store -> ', classesModule.getClasses.length)

      // if classes in store
      alert(`classesModule.getClasses = ${classesModule.getClasses.length}`)

      if(classesModule.getClasses.length > 0) {
        console.log('[created] if classesModule.getClasses.length > 0 ')
        this.API_msg = 'NO API request...'
        // alert(`length -> ${classesModule.getClasses.length}`)
        await this.setDateRange()  // try outside if/else

        // if page is refreshed check session/local storage
        const theClasses = await classesModule.getClasses
        console.log('dash classes -> ', JSON.stringify(theClasses),null)
        this.classes = theClasses
        console.log('CLASSES RETRIEVED FROM STORE .. No API call : ', this.classes)
        this.classesWithPartialAttendance()     
      } else {
        alert('New API request from Dashzz')
      // ALWAYS CALLED - IF IS NOT WORKING - CLASSES NOT GOING INTO THE STORE - PAGE REFRESHES WIPE DATA
      // NEED TO GO BACK TO DASH TO CALL FM AGAIN TO GET THE CLASSES !!!
      this.API_msg = 'New request for classes API.. ' 
      // alert('New FM API call...')
      
      // Check for current pay period
      await this.setDateRange()
      // alert('No CLASSES were found in store. Fresh log in?.... loading classes from API...')
      
      // Needs refactor to sequence loading of data for dash 
      // await this.loadPrivateClasses().then(async() => {
      //   alert('priv loaded!!')
        
      //   await this.loadGroupClasses().then(async() => {
      //     alert('grp loaded!!')
         
      //   })
      // })

      // API v1
      // const promisesArray = await [this.loadPrivateClasses(),this.loadGroupClasses()]

      // API v2
      const promisesArray = await [this.loadPrivateClasses()]

      // await Promise.all(promisesArray).then(() => {
      
      Promise.all(promisesArray).then((r) => {
        console.log('DASH[promises all] -> ', r)
        const p0 = r[0]

        if(p0 === 'undefined') {
          alert('handle lost connection...')
        }

        // const p1 = r[1]

        // if(p0 === undefined && p1 === undefined) {
        //   alert('No classes found for this teacher') 
        //   return 
        // }
     
        // this.getTwoWeekAttendance()
        // await this.checkAttendanceForPreviousTwoWeeks()
        //  await this.checkAttendanceForPreviousTwoWeeks().then(async()=>{
        // alert('SUCCESS FOR CHECK Prev 2 weeks att ??? gonna rerender widgets')   
        this.getCurrentStudents().then((results) => {
          // alert(`BACK : ${JSON.stringify(results)}`)
          this.currentStudents = results
          // this.notesArr = this.sortByDate(this.notes)
          console.log('the notes -> ', this.notesArr)
          this.text = 'Dynamic text'
          const newDataDate = new Date()
          this.lastUpdated = moment(newDataDate)
          // this.rerenderWidgets += 1
          // this.notesArr = this.prepNotes
          // this.prepWidgets()
          // console.log('Rerender finished in else? ', this.rerenderWidgets)
          // alert('Check rerender')   
        })
        //  })

        // this.rerenderWidgets += 1
        // const incompleteAttendance = await classesModule.classesWithIncompleteAttendance
        // console.log('Results incmplete attendance : ', incompleteAttendance)

        // this.existingRecords = await attendanceModule.getAttendance
        // this.numAttendanceRecords = await attendanceModule.getAttendanceLength
        // alert(`DASH - existing records from attendanceModule : ${JSON.stringify(this.existingRecords.length)}`)
      })
      .catch((err) => { console.log('ERR getting Classes [dashboard] -> ', err); this.logout(err) })
        
      // theGroupClasses.then(async() => {})

      // await this.getTwoWeekAttendance()
      // await this.getCurrentStudents()

        // await this.getCurrentStudents().then(async() => {
        //   await this.getTwoWeekAttendance().then(async () => {
        //     alert("FRESH LOGIN OR REFRESH :: pause before missing records call...")
        //     await this.missingRecordsCheck().then(() => {
        //       alert("FRESH LOGIN OR REFRESH :: pause after missing records call...")

        //       this.numStudents = classesModule.getNumStudents
        //       console.log('SFC : ', JSON.stringify(this.currentStudents))
        //       alert('FRESH LOGIN OR REFRESH :: CHECK console post-api classes load...SFC(Students from Classes) ')
        //       this.rerenderWidgets += 1
        //       this.widgetsVisible = true
        //     })
        //   })
        // })

      // Both existing records and current period classes should be loaded by now
      // console.log('EXISTIG CHECK : ', this.existingRecords)
      // await this.missingRecordsCheck()
      // alert(`MISSING records should be ready in dash.mount : ${this.missingRecords}`)
      // this.rerenderWidgets += 1

    }


    // if(this.classes.length < 1){ 
      // No classes in store
      // alert(`Classes from store: ${ classesModule.getClasses }`)
      
      // Two async calls here - private and group classes 
      // Each call will push classes into one event array on the store

      // await this.getEvents() // API calls to get all private and groups
     

      // await this.allClasses()
      // await this.currentAttendanceStats()
      
      // this.numStudents = await classesModule.getNumCurrentStudents()

      
      // const testC = JSON.stringify(this.classes[0][3])
      // alert(`dash.this.getEvents & allClasses finished here..... ${testC}`)

      // API to see if partially complete class attendance
      // await this.previousSubmittedAttendance()

      // Find previously submitted records in current class range
      // this.previousSubmittedAttendance()
  }

  here(){
    alert('alert was closed ....')
  }

  sortByDate(notes){
    alert('works')
    notes.sort((a,b)=>a.displayDate()-b.displayDate());
  }


  closedAlert(e){
    alert(e)
    this.showUpdateAlert = false
    // localStorage.setItem('Update Read', 'true')
  }

  get update() {
    return true
  }

  get attendanceUpToDate() {
    if(this.recentlySubmitted.length - this.currentAttendanceDue.length === 0){
      return true 
    } else {
      return false
    }
  }

  get totalClasses() {
      // alert(' num classes in widgets called ....')
      const totalClasses = classesModule.getClasses
      return totalClasses
    }

  get getNotes() {
    const newNotes = classesModule.getNotes.map(n => n['fieldData'])

    // alert(`NOTES here : ${newNotes}`)
    return newNotes

  }

  get recentlySubmitted() {
    const recentRecords = classesModule.submittedAttendanceForPeriod // only include from the current period
    return recentRecords
  }

  get classesWithIncompleteAttendance() {
    // get index of class in calendar events
    return classesModule.partialCompleteAttendance
  }

  // get attendanceDue() {
  //   this.currentAttendanceDue.filter(c => {
  //   })
  // }

  get currentAttendanceDue() {
    const theStudents = classesModule.studentsFromClasses
    // alert(`getCurrentStudents check console.. returning next..check console ${theStudents}`) // nothing
    return theStudents
  }

  get totalAttendanceDue(){
    return this.currentAttendanceDue.length
  }

  async getCurrentStudents(): Promise<TODO> {

    return new Promise((resolve, reject) => {
      const theStudents = classesModule.studentsFromClasses
      // alert(`getCurrentStudents check console.. returning next ${theStudents}`)// nothing here
      if(theStudents.length){
       // alert(`getCurrentStudents : ${theStudents}` )
        resolve(theStudents)
      } else {
        // alert('problem getting students..')
        reject('problem with students')
      }

    })
  }
    
  
  // prepWidgets(){
  //    this.upcomingClasses = [
  //     {
  //       bgColor: "cyan darken-2",
  //       iconClass: "amber white--text",
  //       icon: "mdi-calendar",
  //       title: "Classes in Schedule",
  //       data: this.totalClasses,
  //       action: {
  //         label: "more",
  //         link: "/calendar"
  //       }
  //     },
  //     {
  //       bgColor: "orange darken-3",
  //       iconClass: "amber white--text",
  //       icon: "mdi-wallet-membership",
  //       title: "Private Classes",
  //       data: classesModule.getPrivateClassesLength,
  //       action: {
  //         label: "more",
  //         link: ""
  //       }
  //     },
  //     //  {
  //     //   bgColor: "purple  lighten-1",
  //     //   iconClass: "cyan white--text",
  //     //   icon: "mdi-wallet-giftcard",
  //     //   title: "Finishing Soon",
  //     //   data: 2,
  //     //   action: {
  //     //     label: "more",
  //     //     link: ""
  //     //   }
  //     // },
  //     // {
  //     //   bgColor: "grey  darken-1",
  //     //   iconClass: "blue lighten-3 white--text",
  //     //   icon: "mdi-wall",
  //     //   title: "Weekly Hours",
  //     //   data: "15",
  //     //   action: {
  //     //     label: "more",
  //     //     link: ""
  //     //   }
  //     // },
  //     {
  //       bgColor: "green  darken-2",
  //       iconClass: "blue lighten-3 white--text",
  //       icon: "mdi-wall",
  //       title: "Notes",
  //       data: classesModule.getNumNotesToTeacher,
  //       action: {
  //         label: "more",
  //         link: ""
  //       }
  //     },
  //     {
  //       bgColor: "purple  lighten-2",
  //       iconClass: "blue lighten-3 white--text",
  //       icon: "mdi-wall",
  //       title: "Attendance Stats",
  //       data: classesModule.getNumNotesToTeacher,
  //       action: {
  //         label: "more",
  //         link: ""
  //       }
  //     },
  //     {
  //       bgColor: "yellow  darken-2",
  //       iconClass: "blue lighten-3 white--text",
  //       icon: "mdi-wall",
  //       title: "Number of Students",
  //       data: classesModule.getNumStudents,
  //       action: {
  //         label: "more",
  //         link: ""
  //       }
  //     }
  //   ];

  // }

  // get prepNotes(){
  //   return this.notes
  // }

  async missingRecordsCheck(){
    console.log('EXISTING IN MISSING : ', JSON.stringify(this.existingRecords))
    console.log('CURR STUDENTS IN MISSING : ', JSON.stringify(this.currentStudents))
    // this.getCurrentStudents,this.getTwoWeekAttendance

    // alert('In missing records')
    // alert('Missing called...')
    // iterate students from current student list (students for elapsed period, eg. yesterday to 2 weeks ago)
    // this.currentStudents.forEach((s) => {
    //   if(s['Student classmates startup::First Name'] !== undefined) {
    //     alert('inside')
    //     s.forEach((p) => {
    //       console.log('Checking for GRP student :', p['Student classmates startup::First Name'])
    //     })
    //   } else {
    //     console.log('Checking student :', s.fname)
    //   }

      // find if student attendance is not in the existingAttendance list
      // ref: https://stackoverflow.com/questions/32965688/comparing-two-arrays-of-objects-and-exclude-the-elements-who-match-values-into
      const theRecords = await this.currentStudents.filter((s: TODO) => {
          // alert(`st : ${JSON.stringify(s)}`)
          return !this.existingRecords.some((r, i) => {
            if(i === this.existingRecords.length -1) {
              console.log('MISSING RECORDS CHECK FINISDED at index : ', i )
              this.rerenderWidgets += 1
            }
            // if(s.sID === r["sID"] && s.class_id === r["class_id"]) {}
            return s.sID === r['fieldData']["_fk_student_id"] && s.class_id === r['fieldData']["class_id"] ; // return the ones with equal id
        });
      });
      // this.missingRecords.push(theRecords)
      this.missingRecords = theRecords
      console.log('THE missing recs result ', JSON.stringify(this.missingRecords))
      // alert('PAUSE N CHECK FOR MISSING RECORDS....')
  }

  async currentAttendanceStats() {
    classesModule.getCurrentAttendanceStats().then((r) => {
      console.log(r)
    })  
  }

  // ADMIN TOOL - maybe set up as option on admin teacher list when selecting to view as teacher
  async setDateRange() {
    // Two date ranges required
    // 1. Range for classes viewable/editable in calendar (1 month ahead)
    // 2. Range used to check for previously submitted attendance (2 weeks back)
    
    // Production
    const now: Date  = new Date()
    // const beginDate = moment(now).subtract(30, 'days').format('MM/DD/YYYY') 
    // const endDate = moment(now).add(30, 'days').format('MM/DD/YYYY') 

    // Development - fake current date to find records in R&D DB
    this.fakeNowMonth = moment(now).subtract(6, 'months').format('MM/DD/YYYY')  // Increase month to set further back
    // alert(`Fake NOW :  ${this.fakeNowMonth}`)

    // Range for classes schedule 
    const beginDate = moment(this.fakeNowMonth).subtract(30, 'days').format('MM/DD/YYYY') 
    const endDate = moment(this.fakeNowMonth).add(30, 'days').format('MM/DD/YYYY') 

    // Range for attendance records check 
    this.yesterday = moment(this.fakeNowMonth).subtract(1, 'day').format('MM/DD/YYYY') 
    this.twoWeeksAndDayAgo = moment(this.yesterday).subtract(14, 'day').format('MM/DD/YYYY') 

    // futureTime.setDate(futureTime.getDate()+30)
    // const pastTime = new Date(new Date().getDate()-10)
    // pastTime.setDate(pastTime)

    // const pastDate = moment(pastTime).subtract(30, 'days').format('MM/DD/YYYY') 
    // const futureDate = moment(pastTime).format('MM/DD/YYYY') 
    this.dateRange = beginDate + '...' + endDate

    // alert(`DATE RANGE SET IN DASH :  ${this.dateRange} `)

  }

  // Use for recently submitted widget? 
  async checkAttendanceForPreviousTwoWeeks() {
    // alert('checkAttendanceForPreviousTwoWeeks called...')
    classesModule.getExistingFmAttendance().then((res) => {
      // alert(`Back from attendance check.. about to set alert and rerender... MSG: ${res}`)
      this.attendanceAlert = 'Attendance check finished...'
      this.rerenderWidgets += 1
    })
  }
  // Gets all records in wp2Attendance for previous 2 weeks
  // Checks all attendance based on teacher_id
  async getTwoWeekAttendance() {
    // const attNum = attendanceModule.getAttendanceLength
    // console.log('dash.getTwoWeekAttendance : NUM of attendance records in store : ', attNum)
    // alert('check')

    // check store first for attendance records
    // if(attendanceModule.getAttendanceLength > 0) return
    // if(attendanceModule.getAttendanceLength < 1) {
    //   alert('In attendance check because fresh login or page refresh')

    //   const startDate = moment(this.dates[0]).format('MM/DD/YYYY') 
    //   const endDate = moment(this.dates[1]).format('MM/DD/YYYY')
    //   const startDate = moment('11/10/2020').format('MM/DD/YYYY')
    //   const endDate = moment('01/21/2021').format('MM/DD/YYYY') 
    //   const dateRangeQuery = startDate + '...' + endDate // Formatted for FMS API 
    //   const fmtoken =  await sessionStorage.getItem('fm-token')
    //   const teacher_FM_ID = await sessionStorage.getItem('fm_id')


    //   const data = {
    //     query: {"query": [{"teacher_id": teacher_FM_ID, "ClassDate": dateRangeQuery}]},
    //     token: fmtoken
    //   }

    //   return attendanceModule.checkAttendanceRecords(data).then(async(r) => {
    //     console.log('Records response from Attendance Module:  ', r)
      
    //     if(r && r == 'No records found') { 
    //       return 
    //     }

    //         console.log('result from attendance call ', JSON.stringify(r))
            
    //         this.checkAttendanceRequests += 1
    //         await this.getCurrentStudents().then(async() => {
    //           await this.missingRecordsCheck().then(()=>{
    //           })
    //         })
       
    //   })  
    // } 
  }
  // Not USED -- check
  async previousSubmittedAttendance() {
    // alert('called previous..')
    // promise ??
    // const theClasses = JSON.parse(JSON.stringify(classesModule.getClasses))
    // const theClasses = JSON.parse(JSON.stringify(classesModule.getClasses))
    const sC = await JSON.stringify(this.classes[0])

    // alert(`Dash.previousSubmittedAttendnace : ${theClasses}`)
    // alert(`Dash.previousSubmittedAttendnace SINGLE CLASS : ${sC}`)

    classesModule.getExistingFmAttendance().then(r => {
      console.log('classesModule.getExistingFmAttendance res : ', r)
      // alert('DASH.previousSubmittedAttendance getExistingFmAttendance FINISHED : check results in console')
    })

    // await Promise.all(theClasses.map(async (c,i) => {
    //   const cs = JSON.parse(JSON.stringify(c['portalData']['Student']))
    //   await Promise.all(c['portalData']['Students'].map(async (s,i) => {
    //     // classesModule.getExistingFmAttendance(s) 
    //     alert(`how is : ${s}`)
    //   }))
    // }))
  }
  // FIX :: After route to DASH after login success 
  // the classes are in added to the store from this function 
  // BUT...when navigate to the API route the classes are added 
  // again causing accumullation of same classes in the store!

  // public async getEvents(){
  //   // Loading Spinner 
  //   await this.loadPrivateClasses()
  //   await this.loadGroupClasses() 

  //   // this.numClasses = await classesModule.getNumClasses
  //   // console.log('NUM CLASSES :', this.numClasses)  
  // }

  // Not currently used 
  changeModDate(s) {
    s["fieldData"]["z_ModifiedOn"] = "12/21/2022 09:49:25" 
    console.log('logDate ', s)
  }

  async setLastModDate() {
    const schedule = JSON.parse(sessionStorage.getItem('events'))
    // Dev function to change one of the mod dates in the returned FM records
    // They were all the same and could not be changed directly in api_CLASSES
    // await this.changeModDate(schedule[2])

    // Returns the latest modified date - check console -> MOD date is incorrect in object??
    const lastModDate = schedule.reduce((a, b) => {
        return new Date(a["fieldData"]["z_ModifiedOn"]) > new Date(b["fieldData"]["z_ModifiedOn"]) ? a : b;
    });
    console.log('Last Mod Date(Dash[setLastModDate]-> reduce: ', lastModDate)
    // Production - simply save last modified record date
    // sessionStorage.setItem('lastModDate', lastModDate['fieldData']['z_ModifiedOn'])

    // Development
    // Format dummy last modified date using Moment.js
    // Add the desired date manually to test that FM polling to sync data is working 
    const adjustedDate = moment(lastModDate['fieldData']['z_ModifiedOn']).format('04/11/2023 10:49:31');    
    sessionStorage.setItem('lastModDate', adjustedDate)




    // schedule.forEach(function (e, i) {
    //     console.log("daFunk -> ", e['fieldData']['scheduleDate'])
    //     console.log("NEW -> ", e['fieldData']['z_ModifiedOn']) // if dates are the same it will be one line
    //     // Next get latest date 
    //   }
    // )

  }

  async loadPrivateClasses(): Promise<TODO> {
    // alert('New api request LPC...')

    // V2 - Adds set range of private classes to the store
    // return new Promise(function(resolve, reject) {

      // TESTING THIS without return 
    // return classesModule.getAllClasses().then((r) => {
      classesModule.getAllClasses().then((r) => {

       // alert('Loading private classes [Dashboard.vue]')
        console.log('THE PRIVATE IN DASH PROMISE ', r)

        // Check for missing data
        this.missingDataAlert  = r.filter(c => { return c['portalData']['class_REGISTRATIONS'].length < 1})
        console.log('MISSING -> ', this.missingDataAlert)

    
        // Set last modified date to Local Storage
        this.setLastModDate()

        // console.log('GET CLASSES FROM STORE IN DASH : ', JSON.stringify(classesModule.getClasses))

      // const cc = JSON.parse(JSON.stringify(classesModule.getClasses)) // Returns 3 privates
      // alert('dash.loadPrivateClasses - check console for scheduled class..returning true to promises.all')
      // this.classes.push(results)

        // return true
        // this.API_CALLS += 1
        // if(this.API_CALLS.length === 2) {
        //   this.getTwoWeekAttendance()
        // }
        // await this.getTwoWeekAttendance().then(async() => {
        // alert("2 week done and missing records should be fixed...")
        //   // await this.missingRecordsCheck().then(() => {
        //   //   alert("pause after missing records call...")
        //   //   this.rerenderWidgets += 1
        //   // })
        // })
          // resolve(true)
      }).catch(e => {
          console.log('ERROR in dash.loadPrivateClasses : ', e)
          // this.logout()
          // reject
          // return false
           // move logout to Promises.all catch in setup?
      }); 
    // });
  }

  // async loadGroupClasses(): Promise<TODO> {
  //   // V2 - Adds set range of private classes to the store
  //   // return new Promise(function(resolve, reject) {
  //     return classesModule.getGroupClasses().then((r) => {
  //       // console.log('dash.loadGroupClasses : returning true to promises.all', classesModule.getClasses)
  //       console.log('THE GROUPS IN DASH PROMISE ', r)
  //       // alert('check group')
  //       // this.classes.push(results)
  //       // return classesModule.getClasses

  //       // this.missingRecordsCheck()
  
  //       // this.API_CALLS += 1
  //       // if(this.API_CALLS.length === 2) {
  //       //   this.getTwoWeekAttendance()
  //       // }

  //       // resolve(r)

  //     }).catch(e => {
  //         console.log('ERROR in dash.loadGroupClasses : ', e)
  //         // reject()

  //         // this.logout()
  //     }); 
  //   // });
  // }

  // Compile private and group
  // async allClasses() { 
  //    console.log('ALL CLASSES ... need to filter for dates only before today to check attendance is up-to-date', this.classes)
  //    const theStudents = await classesModule.studentsFromClasses
  //     this.currentStudents.push(theStudents)
 // }

  async logout(err){
   alert(`Logout err : ${err}`)
    console.log('DASHBOARD: logout')
    // Try window.location to avoid calling functions after logout triggered
    await userModule.logout();
    // router.push('/login')
  }

  async checkAttendanceRecords(){
    // query teacher_id & date_range
    // const pastDateRange = new Date(Date.now() - 12096e5);
    // const futureDateRange = new Date(Date.now() + 12096e5);

    // Example FM Query to check for existing attendance records in current date range
    // Layout: wp2Attendance
    // POST
    // URL: https://{{server}}/fmi/data/v1/databases/ACA database for R&D (2020 10 21)/layouts/WP2Attendance/_find
    // { "query": [{"teacher_id": "T00000475","ClassDate": "11/28/2020...01/20/2021"}] }
  }
}

</script>

<style scoped>


.calendar-card {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: #ffffff;
  border: 1px solid #dadce0;
  border-radius: 4px;
  /* width: 150px;
  height: 150px; */
  padding: 0px;
  /* box-shadow: 0px 1px 1px rgba(0, 0, 0, 0.12), 0px 1px 2px rgba(0, 0, 0, 0.24); */
}

.calendar-card-month {
  font-size: 16px;
  font-weight: bold;
  text-transform: uppercase;
  color: #ffffff;
  background-color: #4285f4;
  padding: 8px 10px;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
  width: 100%;
  text-align: center;
}

.calendar-card-date {
  font-size: 20px;
  font-weight: bold;
  color: #000000;
  padding: 30px 0;
  width: 100%;
  text-align: center;
  border-top: 1px solid #dadce0;
  border-bottom: 1px solid #dadce0;
}

.calendar-card-day {
  font-size: 16px;
  font-weight: bold;
  color: #000000;
  padding: 8px 10px;
  width: 100%;
  text-align: center;
}

/* .calendar-card {
  display: flex;
  align-items: center;
  width: 100%;
  max-width: 350px;
  height: 80px;
  padding: 10px;
  background-color: #f5f5f5;
  border-radius: 5px;
} */

/* .calendar-month {
  font-size: 12px;
  font-weight: bold;
  color: #ffffff;
  text-align: center;
  text-transform: uppercase;
  background-color: #1a73e8;
  padding: 5px;
  width: 100%;
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
} */

/* .calendar-day {
  font-size: 12px;
  font-weight: bold;
  color: #000000;
  text-align: center;
  text-transform: uppercase;
  padding: 5px;
  width: 100%;
  border-bottom-left-radius: 5px;
  border-bottom-right-radius: 5px;
  background-color: #ffffff;
} */

/* .calendar-date {
  font-size: 36px;
  font-weight: bold;
  color: #000000;
  text-align: center;
  padding: 5px;
  border-right: 2px solid #d9d9d9;
  margin-right: 5px;
  line-height: 1;
} */



.single-widget-icon-wrap {
  margin-left: -8px
}
.v-card {
  transition: opacity .6s ease-in-out;
}
.v-card:not(.on-hover) {
  opacity: 0.9;
}

v-alert { background-color: rgb(74 143 150) !important; }
/* v-alert__border { color:  red !important; }
v-alert__icon { color: red !important } */
.v-alert__content {
  color: #395f90;
}

.v-chip .v-chip__content {
    color: #d9e7f5 !important;
}

.updates-table .v-data-table__empty-wrapper {
  padding: 30px !important;
  border: 1px solid #e0e0e0;
}

 .updates-tr {
  color: aliceblue;
 } 
.v-toolbar__title {
  margin-left: 10px;
  color: #6c7172;
}

.v-card {
  min-height: 100%
}

/* .updates-panel{
  padding-left: 0px;
  max-width: 98.3%;
  margin-bottom: 14px;
  background-color: #6dc7ca;
} */
.dash-widget {
  border-radius: 6px;
}
.widget-data {
  margin-left: -16px !important;
}
.recent-widget {
  /* background-color: #8fdbff8f; */
}

p {
  color: #656767;
}

.top-stats {
  margin-bottom: 25px;
}
.widget-numbers { /* position outside the card and make larger */
  height: 50px;
  min-width: 50px;
  width: 30px;
  margin-right: 10px;
  margin-left: 5px;
  top: -32px;
  left: -30px;
  background-color: #018aff!important; /* primary-like blue */
}
.widget-title {
  font-size: 30px;
}
.widget-text {
  font-size: 16px;
  font-style: italic;
}
.widgets-avatar {
  /* background-color: #feae11!important;
  border-color: #e68a01!important; */
}

.tabs {
  background-color: rgb(255, 254, 254);
  padding-top: 0px;
  margin-right: 8px !important;
  /* border-bottom: 1px solid lightgrey !important; */
}

.tab-content { padding: 20px; }
/* not working yet */
.v-tab v-tab--active {
 /* background-color: #fef2b0 !important; */
  box-shadow: #CCC 0 0 1.35em !important;
}
.v-tab:hover {
  background-color: #cbcbcb;
  color: #018aff;
  /* color: white; */
}
pre {
  overflow-x: auto;
  white-space: pre-wrap;
  white-space: -moz-pre-wrap;
  white-space: -pre-wrap;
  white-space: -o-pre-wrap;
  word-wrap: break-word;
}

.text-center{
  align-self: center;
}
.widget-orange {
  background-color: #f9af18!important;
  border-color: #bb7000!important;
}
.dash-table{
  border-radius: 8px;
  /* background-color: rgb(178 178 179 / 4%); */
  margin-top: 20px;
}
.attedance-due-card {
  /* margin-top: 0px; */
  /* margin-bottom: 3px; */
  border-radius: 0px;
  border-bottom: 3px solid #f6f7f7;
}

.project.complete{
  border-left: 4px solid #3CD1C2;
}
.project.ongoing{
  border-left: 4px solid orange
}
.project.overdue{
  border-left: 4px solid tomato;
}

</style>
