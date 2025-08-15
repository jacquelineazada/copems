<template>
  <v-card flat>
    <v-layout>
      <v-main class="main-content">
        <v-toolbar color="transparent" flat>
          <v-toolbar-title class="toolbar-title"
            >Building Permit Applicant Details</v-toolbar-title
          >
        </v-toolbar>

        <v-container fluid class="content-wrapper">
          <v-card class="header-card" flat>
            <v-card-text class="d-flex align-center">
              <v-avatar color="#bbdefb" size="56">
                <span class="text-h5 font-weight-bold">JM</span>
              </v-avatar>
              <div class="ml-4">
                <h1 class="header-title">Jm Deguzman</h1>
                <p class="header-subtitle">jimdeguzman@gmail.com</p>
                <p class="header-subtitle">BP-2023-8888-001</p>
              </div>
              <v-spacer></v-spacer>
              <v-chip size="default" color="warning" variant="tonal" class="status-chip">
                <v-icon start size="small">mdi-clock-outline</v-icon>
                Building Inspection
              </v-chip>
            </v-card-text>
          </v-card>

          <v-row>
            <v-col cols="12" lg="8">
              <v-card class="section-card" flat>
                <v-card-title class="section-title">Applicant Information</v-card-title>
                <v-card-text>
                  <v-row>
                    <v-col cols="12" md="6">
                      <div class="info-block">
                        <div class="info-label">Applicant Name</div>
                        <div class="info-value">Jm Deguzman</div>
                      </div>
                      <div class="info-block">
                        <div class="info-label">Project Location</div>
                        <div class="info-value">San Felipe, Deca II Naga City</div>
                      </div>
                    </v-col>
                    <v-col cols="12" md="6">
                      <div class="info-block">
                        <div class="info-label">Project Name</div>
                        <div class="info-value">Commercial</div>
                      </div>
                    </v-col>
                  </v-row>
                </v-card-text>
              </v-card>

              <v-card class="section-card" flat>
                <v-card-title class="section-title">Property Details</v-card-title>
                <v-card-text>
                  <v-row>
                    <v-col cols="12" md="6">
                      <div class="info-block">
                        <div class="info-label">Property Type</div>
                        <div class="info-value">Commercial Building</div>
                      </div>
                      <div class="info-block">
                        <div class="info-label">Floor Area</div>
                        <div class="info-value">250 sq.m</div>
                      </div>
                      <div class="info-block">
                        <div class="info-label">Property Address</div>
                        <div class="info-value">
                          456 Commercial Avenue, San Felipe, Deca II Naga City
                        </div>
                      </div>
                    </v-col>
                    <v-col cols="12" md="6">
                      <div class="info-block">
                        <div class="info-label">Building Use</div>
                        <div class="info-value">Retail Store</div>
                      </div>
                      <div class="info-block">
                        <div class="info-label">Number of Floors</div>
                        <div class="info-value">2 Floors</div>
                      </div>
                      <div class="info-block">
                        <div class="info-label">Lot Area</div>
                        <div class="info-value">300 sq.m</div>
                      </div>
                    </v-col>
                  </v-row>
                </v-card-text>
              </v-card>

              <v-card class="section-card" flat>
                <v-card-title class="section-title">Inspector Schedule</v-card-title>
                <v-table class="inspector-table">
                  <thead>
                    <tr>
                      <th class="text-left text-subtitle-2">Inspection Type</th>
                      <th class="text-left text-subtitle-2">Status</th>
                      <th class="text-left text-subtitle-2">Inspector Name</th>
                      <th class="text-left text-subtitle-2">Actions</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="item in inspectorSchedule" :key="item.type">
                      <td>{{ item.type }}</td>
                      <td>
                        <v-chip
                          :class="`status-chip-${item.status.toLowerCase()}`"
                          label
                          size="small"
                        >
                          {{ item.status }}
                        </v-chip>
                      </td>
                      <td>{{ item.inspector }}</td>
                      <td>
                        <v-btn
                          color="#2563EB"
                          variant="text"
                          size="small"
                          @click="showScheduleApproved"
                        >
                          View Details
                        </v-btn>
                      </td>
                    </tr>
                  </tbody>
                </v-table>
              </v-card>
            </v-col>

            <v-col cols="12" lg="4">
              <v-card class="section-card" flat>
                <v-card-title class="section-title">Inspection Schedule</v-card-title>
                <v-card-text>
                  <div class="summary-item">
                    <span class="info-label">Date</span>
                    <span class="info-value font-weight-medium">January 15,2025</span>
                  </div>
                  <div class="summary-item mt-4">
                    <span class="info-label">Time</span>
                    <span class="info-value">10:30am</span>
                  </div>
                  <div class="summary-item mt-4">
                    <span class="info-label">Inspection Status</span>
                    <v-chip
                      size="small"
                      color="warning"
                      variant="tonal"
                      class="status-chip"
                    >
                      Pending Schedule
                    </v-chip>
                  </div>
                </v-card-text>
              </v-card>
            </v-col>
          </v-row>
        </v-container>

        <v-dialog v-model="scheduleApprovedDialog" max-width="600">
          <v-card class="schedule-approved-card">
            <v-card-title class="d-flex justify-space-between align-center">
              <div class="d-flex align-center">
                <v-icon color="#16a34a" class="mr-2">mdi-check-circle-outline</v-icon>
                <span class="text-h6 font-weight-bold">Schedule Approved</span>
              </div>
              <v-btn icon @click="scheduleApprovedDialog = false" size="small">
                <v-icon>mdi-close</v-icon>
              </v-btn>
            </v-card-title>
            <v-card-text class="pa-6">
              <v-row>
                <v-col cols="6">
                  <div class="pop-up-details-block">
                    <div class="pop-up-details-label">Inspection Date</div>
                    <div class="pop-up-details-value">January 15, 2025</div>
                  </div>
                  <div class="pop-up-details-block mt-4">
                    <div class="pop-up-details-label">Architectural Works</div>
                    <div class="pop-up-details-value">Eng. Joyce Oberos</div>
                  </div>
                  <div class="pop-up-details-block mt-4">
                    <div class="pop-up-details-label">Electrical Works</div>
                    <div class="pop-up-details-value">Eng. Bernadette Veroza</div>
                  </div>
                </v-col>
                <v-col cols="6">
                  <div class="pop-up-details-block">
                    <div class="pop-up-details-label">Inspection Date</div>
                    <div class="pop-up-details-value">January 15, 2025</div>
                  </div>
                  <div class="pop-up-details-block mt-4">
                    <div class="pop-up-details-label">Civil/Structural Works</div>
                    <div class="pop-up-details-value">Eng. Roberto Martinez</div>
                  </div>
                  <div class="pop-up-details-block mt-4">
                    <div class="pop-up-details-label">Sanitary Plumbing Works</div>
                    <div class="pop-up-details-value">Eng. Andrew Villapane</div>
                  </div>
                </v-col>
              </v-row>
            </v-card-text>
            <v-card-actions class="d-flex justify-end pr-6 pb-6">
              <v-btn color="#16a34a" variant="flat">
                <v-icon start>mdi-email-send-outline</v-icon>
                Send Schedule
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-main>
    </v-layout>
  </v-card>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const inspectorSchedule = ref([
      {
        type: "Architectural Works",
        status: "Approved",
        inspector: "Eng. Joyce Oberos",
      },
      {
        type: "Civil/Structural Works",
        status: "Approved",
        inspector: "Eng. Roberto Martinez",
      },
      {
        type: "Electrical Works",
        status: "Approved",
        inspector: "Eng. Bernadette Veroza",
      },
      {
        type: "Sanitary Plumbing Works",
        status: "Approved",
        inspector: "Eng. Andrew Villapane",
      },
    ]);

    const scheduleApprovedDialog = ref(false);

    const showScheduleApproved = () => {
      scheduleApprovedDialog.value = true;
    };

    return {
      inspectorSchedule,
      scheduleApprovedDialog,
      showScheduleApproved,
    };
  },
};
</script>

<style scoped>
/* ===================================== */
/* General Layout & Theme */
/* ===================================== */
.main-content {
  background-color: #f8f9fa; /* Soft, light grey background */
}
.toolbar-title {
  font-weight: 600;
  font-size: 1.2rem;
  color: #344054;
}
.content-wrapper {
  max-width: 1600px;
  margin: 0 auto;
  padding: 0 24px 24px 24px;
}

/* ===================================== */
/* Header Card */
/* ===================================== */
.header-card {
  background-color: #ffffff;
  border-radius: 12px;
  margin-bottom: 24px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.02);
  border: 1px solid #eaecf0;
}
.header-title {
  font-size: 1.5rem;
  font-weight: 600;
  color: #101828;
  line-height: 1.2;
}
.header-subtitle {
  color: #667085;
  font-size: 0.9rem;
}

/* ===================================== */
/* Section Cards */
/* ===================================== */
.section-card {
  background-color: #ffffff;
  border-radius: 12px;
  margin-bottom: 24px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.02);
  border: 1px solid #eaecf0;
}
.section-title {
  font-size: 1rem;
  font-weight: 600;
  color: #101828;
  padding: 16px 24px 8px 24px;
}
.v-card-text {
  padding: 8px 24px 16px 24px;
}

/* ===================================== */
/* Information Blocks */
/* ===================================== */
.info-block {
  margin-bottom: 1.25rem;
}
.info-block:last-child {
  margin-bottom: 0;
}
.info-label {
  font-size: 0.875rem;
  font-weight: 500;
  color: #667085;
  margin-bottom: 6px;
}
.info-value {
  font-size: 0.95rem;
  font-weight: 500;
  color: #344054;
}

/* ===================================== */
/* Inspector Table */
/* ===================================== */
.inspector-table th {
  font-weight: 600 !important;
  color: #4a4a4a !important;
  background-color: #f5f5f5 !important;
  border-bottom: 1px solid #e0e0e0;
}
.inspector-table td {
  font-weight: 400 !important;
  color: #333333;
  border-bottom: 1px solid #e0e0e0;
}
.v-table__wrapper > table > tbody > tr:last-child > td {
  border-bottom: none !important;
}

/* ===================================== */
/* Status Chips */
/* ===================================== */
.status-chip-pending {
  background-color: #fef9c3;
  color: #f59e0b;
  font-weight: 500;
  border-radius: 16px;
}

.status-chip-approved {
  background-color: #d1fae5;
  color: #059669;
  font-weight: 500;
  border-radius: 16px;
}

.status-chip-rejected {
  background-color: #fee2e2;
  color: #ef4444;
  font-weight: 500;
  border-radius: 16px;
}

/* ===================================== */
/* Summary & Timeline (Now Inspection Schedule) */
/* ===================================== */
.summary-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.status-chip {
  font-weight: 500;
}

/* ===================================== */
/* Schedule Approved Pop-up Styles */
/* ===================================== */
.schedule-approved-card {
  border-radius: 12px;
}
.pop-up-details-block {
  margin-bottom: 0.5rem;
}
.pop-up-details-label {
  font-size: 0.875rem;
  font-weight: 500;
  color: #667085;
}
.pop-up-details-value {
  font-size: 0.95rem;
  font-weight: 500;
  color: #344054;
}
</style>
