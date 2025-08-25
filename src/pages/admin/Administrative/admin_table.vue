<template>
  <v-card>
    <v-layout class="h-screen">
      <v-navigation-drawer v-model="drawer" :rail="rail" permanent @click="rail = false">
        <v-list>
          <v-list-item
            prepend-avatar="https://scontent.fwnp1-1.fna.fbcdn.net/v/t39.30808-6/482007057_953929396944205_496784858672308185_n.jpg?_nc_cat=102&ccb=1-7&_nc_sid=a5f93a&_nc_eui2=AeF3X7hm2ckriTf1-Bb5gNwhfMhmxxDF2Z18yGbHEMXZnS_SYFwo5FDnvG3qtrlx9DhRLvapomr0MD-fhRgSmoPW&_nc_ohc=v8O88NzBvuUQ7kNvwFnBIh7&_nc_oc=AdkMqwh_xy2CJbS7bdcvKQthrGkxfIU0vCgrH2ZVbbBnA6Np0dbxXdNN6IXhypXv0kI&_nc_zt=23&_nc_ht=scontent.fwnp1-1.fna&_nc_gid=pAhEG4OR1_QrK2dAYVpnug&oh=00_AfVz-qWewbXd1nBdAknpRHuxBCTdvevhzQH7e3h1PGBRWg&oe=68A378B4"
            title="Jacqueline"
          >
            <template v-slot:append>
              <v-btn
                icon="mdi-chevron-left"
                variant="text"
                @click.stop="rail = !rail"
              ></v-btn>
            </template>
          </v-list-item>
        </v-list>

        <v-divider></v-divider>

        <v-list density="compact" nav>
          <v-list-item
            prepend-icon="mdi-home-city"
            title="Home"
            value="home"
          ></v-list-item>
          <v-list-item
            prepend-icon="mdi-office-building"
            title="Building Permit"
            value="building_permit"
          ></v-list-item>
          <v-list-item
            prepend-icon="mdi-file-document-outline"
            title="Occupancy Permit"
            value="occupancy_permit"
          ></v-list-item>
          <v-list-item
            prepend-icon="mdi-clipboard-list-outline"
            title="Compliance Monitoring"
            value="compliance_monitoring"
          ></v-list-item>
        </v-list>

        <template v-slot:append>
          <v-list density="compact" nav>
            <v-list-item
              prepend-icon="mdi-logout"
              title="Logout"
              value="logout"
            ></v-list-item>
          </v-list>
        </template>
      </v-navigation-drawer>

      <v-main>
        <v-toolbar color="white">
          <v-toolbar-title class="pl-4">Occupancy Permit Applicants</v-toolbar-title>
          <v-spacer></v-spacer>
          <div class="d-flex flex-column align-end pr-4"></div>
        </v-toolbar>

        <v-container fluid>
          <v-row>
            <v-col cols="12" sm="6" md="3">
              <v-card class="status-card" color="#6394FF">
                <div class="d-flex justify-space-between align-center">
                  <div>
                    <div class="text-subtitle-1">Total Applicants</div>
                    <div class="card-number-total mt-2">3</div>
                  </div>
                  <v-icon size="48" color="#FFFFFF">mdi-account-group-outline</v-icon>
                </div>
              </v-card>
            </v-col>
            <v-col cols="12" sm="6" md="3">
              <v-card class="status-card" color="#FEF9C3">
                <div class="d-flex justify-space-between align-center">
                  <div>
                    <div class="text-subtitle-1">Pending</div>
                    <div class="card-number-pending mt-2">1</div>
                  </div>
                  <v-icon size="48" color="#FFFFFF">mdi-clock-outline</v-icon>
                </div>
              </v-card>
            </v-col>
            <v-col cols="12" sm="6" md="3">
              <v-card class="status-card" color="#41E27D">
                <div class="d-flex justify-space-between align-center">
                  <div>
                    <div class="text-subtitle-1">Approved</div>
                    <div class="card-number-approved mt-2">1</div>
                  </div>
                  <v-icon size="48" color="#FFFFFF">mdi-check-circle-outline</v-icon>
                </div>
              </v-card>
            </v-col>
            <v-col cols="12" sm="6" md="3">
              <v-card class="status-card" color="#FFAAAA">
                <div class="d-flex justify-space-between align-center">
                  <div>
                    <div class="text-subtitle-1">Declined</div>
                    <div class="card-number-declined mt-2">1</div>
                  </div>
                  <v-icon size="48" color="#FFFFFF">mdi-alert-circle-outline</v-icon>
                </div>
              </v-card>
            </v-col>
          </v-row>

          <v-row class="mt-4">
            <v-col cols="12">
              <v-card class="pa-2" flat>
                <v-row align="center" no-gutters>
                  <v-col cols="12" md="8" class="d-flex align-center">
                    <v-text-field
                      density="compact"
                      variant="outlined"
                      label="Search applicants..."
                      prepend-inner-icon="mdi-magnify"
                      hide-details
                      class="flex-grow-1"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" md="4" class="text-right d-flex justify-end">
                    <v-btn color="#2563EB" variant="flat" class="ml-2">
                      <v-icon left>mdi-filter-variant</v-icon>
                      Filter
                    </v-btn>
                  </v-col>
                </v-row>
              </v-card>
            </v-col>
          </v-row>

          <v-row class="mt-4">
            <v-col cols="12">
              <v-card class="elevation-1">
                <v-table class="applicants-table">
                  <thead>
                    <tr>
                      <th class="text-left text-subtitle-2">Applicant Name</th>
                      <th class="text-left text-subtitle-2">Application Number</th>
                      <th class="text-left text-subtitle-2">Date Submitted</th>
                      <th class="text-left text-subtitle-2">Status</th>
                      <th class="text-left text-subtitle-2">Action</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr>
                      <td>
                        <v-avatar
                          size="36"
                          class="mr-2 avatar-style"
                          style="background-color: #bbdefb; color: #1e88e5"
                          >JA</v-avatar
                        >
                        Jacqueline Azada
                      </td>
                      <td>BP-2024-808123-T</td>
                      <td>Jan 15, 2024</td>
                      <td>
                        <v-chip class="status-chip-pending" label size="small"
                          >Pending</v-chip
                        >
                      </td>
                      <td>
                        <v-btn color="#2563EB" variant="tonal" size="small"
                          >View Details</v-btn
                        >
                      </td>
                    </tr>
                    <tr>
                      <td>
                        <v-avatar
                          size="36"
                          class="mr-2 avatar-style"
                          style="background-color: #c8e6c9; color: #43a047"
                          >SG</v-avatar
                        >
                        Sarah Geronimo
                      </td>
                      <td>BP-2024-808234-T</td>
                      <td>Jan 16, 2024</td>
                      <td>
                        <v-chip class="status-chip-approved" label size="small"
                          >Approved</v-chip
                        >
                      </td>
                      <td>
                        <v-btn color="#2563EB" variant="tonal" size="small"
                          >View Details</v-btn
                        >
                      </td>
                    </tr>
                    <tr>
                      <td>
                        <v-avatar
                          size="36"
                          class="mr-2 avatar-style"
                          style="background-color: #ffcdd2; color: #e53935"
                          >MP</v-avatar
                        >
                        Michael Padilla
                      </td>
                      <td>BP-2024-808345-T</td>
                      <td>Jan 17, 2024</td>
                      <td>
                        <v-chip class="status-chip-returned" label size="small"
                          >Declined</v-chip
                        >
                      </td>
                      <td>
                        <v-btn color="#2563EB" variant="tonal" size="small"
                          >View Details</v-btn
                        >
                      </td>
                    </tr>
                  </tbody>
                </v-table>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
      </v-main>
    </v-layout>
  </v-card>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const drawer = ref(true);
    const rail = ref(true);

    return {
      drawer,
      rail,
    };
  },
};
</script>

<style scoped>
/* Navigation Drawer */
.v-navigation-drawer {
  background-color: #ffffff;
  transition: all 0.2s ease;
}

.v-list-item {
  transition: all 0.1s ease;
  font-weight: 500;
  color: #000000;
}

.v-list-item:hover {
  background-color: #acd0ff;
}

.v-divider {
  border-color: #ffffff;
}

/* Main Content Area */
.v-main {
  background-color: #ffffff !important;
}

/* Toolbar */
.v-toolbar {
  color: #333;
}

.v-toolbar-title {
  padding-left: 16px;
  font-weight: normal;
}

.v-toolbar .d-flex {
  padding-right: 16px;
}

/* Dashboard Cards */
.status-card {
  border-radius: 12px;
  transition: transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  padding: 16px;
  color: #000;
}

.status-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 12px rgba(0, 0, 0, 0.1);
}

.card-number-total {
  font-weight: 600;
  font-size: 2.1rem;
  line-height: 2rem;
  color: #003fbd; /* Darker than #6394FF */
}

.card-number-pending {
  font-weight: 600;
  font-size: 2.1rem;
  line-height: 2rem;
  color: #c7ad00; /* Darker than #FEF9C3 */
}

.card-number-approved {
  font-weight: 600;
  font-size: 2.1rem;
  line-height: 2rem;
  color: #006423; /* Darker than #41E27D */
}

.card-number-declined {
  font-weight: 600;
  font-size: 2.1rem;
  line-height: 2rem;
  color: #851414; /* Darker than #FFAAAA */
}

/* Data Table */
.applicants-table {
  background-color: #ffffff;
}

.applicants-table th {
  font-weight: 600 !important;
  color: #4a4a4a !important;
  background-color: #f5f5f5 !important;
}

.applicants-table td {
  font-weight: 400 !important;
  color: #333333;
}

/* Status Chips */
.status-chip-pending {
  background-color: #fef9c3;
  color: #ffde09; /* A darker yellow for text */
  font-weight: 500;
  border-radius: 16px;
}

.status-chip-approved {
  background-color: #47e983;
  color: #478760; /* A darker green for text */
  font-weight: 500;
  border-radius: 16px;
}

.status-chip-returned {
  background-color: #ffa0a0;
  color: #9f4444; /* A darker red for text */
  font-weight: 500;
  border-radius: 16px;
}

/* Avatars */
.avatar-style {
  font-weight: bold;
}

/* Search and Filter */
.v-text-field {
  max-width: 300px;
}

.v-btn {
  font-weight: 500;
}

.v-container {
  padding: 14px 32px;
}
</style>
