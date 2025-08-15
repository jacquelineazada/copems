<template>
  <v-card>
    <v-layout>
      <v-main class="main-content">
        <v-container fluid class="content-wrapper">
          <v-row justify="center">
            <v-col cols="12" sm="6" md="3">
              <v-card class="status-card" color="#6394FF">
                <div class="d-flex justify-space-between align-center">
                  <div>
                    <div class="text-subtitle-1">Total Applicants</div>
                    <div class="card-number-total mt-2">4</div>
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
                    <div class="card-number-pending mt-2">2</div>
                  </div>
                  <v-icon size="48" color="#FFFFFF">mdi-clock-outline</v-icon>
                </div>
              </v-card>
            </v-col>
            <v-col cols="12" sm="6" md="3">
              <v-card class="status-card" color="#41E27D">
                <div class="d-flex justify-space-between align-center">
                  <div>
                    <div class="text-subtitle-1">Passed</div>
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
                    <div class="text-subtitle-1">Violation</div>
                    <div class="card-number-declined mt-2">1</div>
                  </div>
                  <v-icon size="48" color="#FFFFFF">mdi-alert-circle-outline</v-icon>
                </div>
              </v-card>
            </v-col>
          </v-row>

          <v-row class="mt-4" justify="center">
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

          <v-row class="mt-4" justify="center">
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
                    <tr
                      v-for="applicant in applicants"
                      :key="applicant.applicationNumber"
                    >
                      <td>
                        <v-avatar
                          size="36"
                          class="mr-2 avatar-style"
                          :style="{
                            backgroundColor: applicant.avatarColor,
                            color: applicant.avatarTextColor,
                          }"
                        >
                          {{ applicant.initials }}
                        </v-avatar>
                        {{ applicant.name }}
                      </td>
                      <td>{{ applicant.applicationNumber }}</td>
                      <td>{{ applicant.inspectionDate }}</td>
                      <td>
                        <v-chip
                          :class="`status-chip-${applicant.status.toLowerCase()}`"
                          label
                          size="small"
                        >
                          {{ applicant.status }}
                        </v-chip>
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
    const applicants = ref([
      {
        name: "Jacqueline Azada",
        initials: "JA",
        applicationNumber: "BP-2024-808123-T",
        inspectionDate: "Jan 15, 2024",
        status: "Pending",
        avatarColor: "#bbdefb",
        avatarTextColor: "#1e88e5",
      },
      {
        name: "Sarah Geronimo",
        initials: "SG",
        applicationNumber: "BP-2024-808234-T",
        inspectionDate: "Jan 16, 2024",
        status: "Passed",
        avatarColor: "#c8e6c9",
        avatarTextColor: "#43a047",
      },
      {
        name: "Michael Padilla",
        initials: "MP",
        applicationNumber: "BP-2024-808345-T",
        inspectionDate: "Jan 17, 2024",
        status: "Violation",
        avatarColor: "#ffcdd2",
        avatarTextColor: "#e53935",
      },
      {
        name: "James Smith",
        initials: "JS",
        applicationNumber: "BP-2024-808456-T",
        inspectionDate: "Jan 18, 2024",
        status: "Pending",
        avatarColor: "#e3f2fd",
        avatarTextColor: "#2196f3",
      },
    ]);

    return {
      applicants,
    };
  },
};
</script>

<style scoped>
/* Main Content Area */
.main-content {
  background-color: #f8f9fa !important;
}

/* Content wrapper for padding and max-width */
.content-wrapper {
  max-width: 1600px;
  margin: 0 auto;
  padding: 24px;
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
  border-radius: 12px;
  border: 1px solid #e0e0e0;
}

.applicants-table th {
  font-weight: 600 !important;
  color: #4a4a4a !important;
  background-color: #f5f5f5 !important;
  border-bottom: 1px solid #e0e0e0;
}

.applicants-table td {
  font-weight: 400 !important;
  color: #333333;
  border-bottom: 1px solid #e0e0e0;
}

/* Status Chips */
.status-chip-pending {
  background-color: #fef9c3;
  color: #c7ad00;
  font-weight: 500;
  border-radius: 16px;
}
.status-chip-passed {
  background-color: #d1fae5;
  color: #059669;
  font-weight: 500;
  border-radius: 16px;
}
.status-chip-violation {
  background-color: #fee2e2;
  color: #ef4444;
  font-weight: 500;
  border-radius: 16px;
}

/* Avatars */
.avatar-style {
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
