<template>
  <v-card flat>
    <v-layout>
      <v-main class="main-content">
        <v-toolbar color="transparent" flat>
          <v-breadcrumbs :items="breadcrumbs" class="pa-0">
            <template v-slot:divider>
              <v-icon icon="mdi-chevron-right"></v-icon>
            </template>
          </v-breadcrumbs>
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
              <div class="text-right">
                <v-chip
                  size="default"
                  color="warning"
                  variant="tonal"
                  class="status-chip"
                >
                  <v-icon start size="small">mdi-clock-outline</v-icon>
                  Building Inspection
                </v-chip>
                <div class="submitted-text mt-1">Submitted: Jan 15, 2024</div>
              </div>
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
                <v-card-title class="section-title">Inspection Results</v-card-title>
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
                    <tr v-for="item in inspectionResults" :key="item.type">
                      <td>{{ item.type }}</td>
                      <td>
                        <v-chip class="status-chip-pending" label size="small">
                          {{ item.status }}
                        </v-chip>
                      </td>
                      <td>{{ item.inspector }}</td>
                      <td>
                        <v-btn color="#2563EB" variant="text" size="small">
                          View Report
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
                    <span class="info-value font-weight-medium">10:30am</span>
                  </div>
                  <div class="summary-item mt-4">
                    <span class="info-label">Inspection Status</span>
                    <v-chip
                      size="small"
                      color="warning"
                      variant="tonal"
                      class="status-chip"
                    >
                      Pending Result
                    </v-chip>
                  </div>
                </v-card-text>
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
    // Data for breadcrumbs
    const breadcrumbs = ref([
      {
        title: "Occupancy Permit Applicants",
        disabled: false,
        href: "#",
      },
      {
        title: "Inspection Report",
        disabled: true,
      },
    ]);

    // Data for the inspection results table
    const inspectionResults = ref([
      {
        type: "Architectural Works",
        status: "Pending",
        inspector: "Eng. Joyce Oberos",
      },
      {
        type: "Civil/Structural Works",
        status: "Pending",
        inspector: "Eng. Roberto Martinez",
      },
      {
        type: "Electrical Works",
        status: "Pending",
        inspector: "Eng. Bernadette Veroza",
      },
      {
        type: "Sanitary Plumbing Works",
        status: "Pending",
        inspector: "Eng. Andrew Villapane",
      },
    ]);

    return {
      breadcrumbs,
      inspectionResults,
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
.v-breadcrumbs {
  color: #667085;
}
.v-breadcrumbs .v-breadcrumbs-item--disabled {
  color: #101828;
  font-weight: 500;
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
  margin: 0;
  line-height: 1.5;
}
.submitted-text {
  font-size: 0.8rem;
  color: #667085;
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
  background-color: #f9fafb !important;
  border-bottom: 1px solid #e0e0e0 !important;
}
.inspector-table td {
  font-weight: 400 !important;
  color: #333333;
  border-bottom: 1px solid #e0e0e0;
}
.v-table__wrapper > table > tbody > tr:last-child > td {
  border-bottom: none !important;
}
.v-btn {
  text-transform: none;
}

/* ===================================== */
/* Status Chips */
/* ===================================== */
.status-chip-pending {
  background-color: #fef9c3;
  color: #f59e0b; /* A darker yellow for text */
  font-weight: 500;
  border-radius: 16px;
}

/* ===================================== */
/* Inspection Schedule Side Card */
/* ===================================== */
.summary-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.status-chip {
  font-weight: 500;
}
</style>
