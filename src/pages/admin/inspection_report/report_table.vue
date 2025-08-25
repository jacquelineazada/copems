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
          <v-toolbar-title class="pl-4">Building Inspection Report</v-toolbar-title>
          <v-spacer></v-spacer>
          <div class="d-flex flex-column align-end pr-4"></div>
        </v-toolbar>

        <v-container fluid>
          <v-row>
            <v-col cols="12" sm="6" md="3">
              <v-card class="status-card" color="#2563EB">
                <div class="d-flex justify-space-between align-center">
                  <div>
                    <div class="text-subtitle-1 text-white">Total Applicants</div>
                    <div class="card-number-total mt-2">3</div>
                  </div>
                  <v-icon size="48" color="#FFFFFF">mdi-account-group</v-icon>
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
                  <v-icon size="48" color="#A16207">mdi-clock-outline</v-icon>
                </div>
              </v-card>
            </v-col>
            <v-col cols="12" sm="6" md="3">
              <v-card class="status-card" color="#D9F9E5">
                <div class="d-flex justify-space-between align-center">
                  <div>
                    <div class="text-subtitle-1">Passed</div>
                    <div class="card-number-approved mt-2">1</div>
                  </div>
                  <v-icon size="48" color="#15803D">mdi-check-circle</v-icon>
                </div>
              </v-card>
            </v-col>
            <v-col cols="12" sm="6" md="3">
              <v-card class="status-card" color="#FFE2E5">
                <div class="d-flex justify-space-between align-center">
                  <div>
                    <div class="text-subtitle-1">Violation</div>
                    <div class="card-number-violation mt-2">1</div>
                  </div>
                  <v-icon size="48" color="#DC2626">mdi-alert-circle</v-icon>
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
                    <v-btn color="#2563EB" variant="flat" class="ml-2 text-white">
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
                      <th class="text-left text-subtitle-2">Inspection Date</th>
                      <th class="text-left text-subtitle-2">Status</th>
                      <th class="text-left text-subtitle-2">Action</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="applicant in applicants" :key="applicant.appNumber">
                      <td>
                        <v-avatar
                          size="36"
                          class="mr-2 avatar-style"
                          :style="{
                            backgroundColor: applicant.avatarBg,
                            color: applicant.avatarColor,
                          }"
                        >
                          {{ applicant.initials }}
                        </v-avatar>
                        {{ applicant.name }}
                      </td>
                      <td>{{ applicant.appNumber }}</td>
                      <td>{{ applicant.date }}</td>
                      <td>
                        <v-chip
                          :class="getChipClass(applicant.status)"
                          label
                          size="small"
                        >
                          {{ applicant.status }}
                        </v-chip>
                      </td>
                      <td>
                        <v-btn
                          v-if="applicant.status === 'Pending'"
                          color="#2563EB"
                          variant="tonal"
                          size="small"
                          to="ReportPending"
                        >
                          View Details
                        </v-btn>
                        <v-btn
                          v-else-if="applicant.status === 'Passed'"
                          color="#15803D"
                          variant="tonal"
                          size="small"
                          to="ReportApproved"
                        >
                          View Details
                        </v-btn>
                        <v-btn
                          v-else-if="applicant.status === 'Violation'"
                          color="#DC2626"
                          variant="tonal"
                          size="small"
                          to="ReportPV"
                        >
                          View Details
                        </v-btn>
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

    const applicants = ref([
      {
        initials: "JA",
        name: "Jacqueline Azada",
        appNumber: "BP-2024-808123-T",
        date: "Jan 15, 2024",
        status: "Pending",
        avatarBg: "#FEF9C3",
        avatarColor: "#A16207",
      },
      {
        initials: "SG",
        name: "Sarah Geronimo",
        appNumber: "BP-2024-808234-T",
        date: "Jan 16, 2024",
        status: "Passed",
        avatarBg: "#D9F9E5",
        avatarColor: "#15803D",
      },
      {
        initials: "MP",
        name: "Michael Padilla",
        appNumber: "BP-2024-808345-T",
        date: "Jan 17, 2024",
        status: "Violation",
        avatarBg: "#FFE2E5",
        avatarColor: "#DC2626",
      },
    ]);

    const getChipClass = (status) => {
      switch (status) {
        case "Passed":
          return "status-chip-approved";
        case "Pending":
          return "status-chip-pending";
        case "Violation":
          return "status-chip-violation";
        default:
          return "";
      }
    };

    return {
      drawer,
      rail,
      applicants,
      getChipClass,
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
  background-color: #e3f2fd;
}

/* Main Content Area */
.v-main {
  background-color: #f8f9fa !important;
}

/* Toolbar */
.v-toolbar {
  color: #333;
}

.v-toolbar-title {
  padding-left: 16px;
  font-weight: 600;
}

/* Dashboard Cards */
.status-card {
  border-radius: 12px;
  transition: transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  padding: 20px;
}

.status-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 12px rgba(0, 0, 0, 0.1);
}

.card-number-total,
.card-number-pending,
.card-number-approved,
.card-number-violation {
  font-weight: 700;
  font-size: 2.25rem;
  line-height: 2.5rem;
}

.card-number-total {
  color: #ffffff;
}
.card-number-pending {
  color: #a16207;
}
.card-number-approved {
  color: #15803d;
}
.card-number-violation {
  color: #dc2626;
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
  font-weight: 500 !important;
  color: #333333;
  vertical-align: middle;
}

/* Status Chips */
.status-chip-pending,
.status-chip-approved,
.status-chip-violation {
  font-weight: 500;
  border-radius: 16px;
  padding: 4px 12px;
}

.status-chip-pending {
  background-color: #fef9c3;
  color: #a16207;
}

.status-chip-approved {
  background-color: #d9f9e5;
  color: #15803d;
}

.status-chip-violation {
  background-color: #ffe2e5;
  color: #dc2626;
}

/* Avatars */
.avatar-style {
  font-weight: bold;
}

/* Search and Filter */
.v-text-field {
  max-width: 400px;
}

.v-btn {
  font-weight: 500;
  text-transform: none;
}

.v-container {
  padding: 14px 32px;
}
</style>
