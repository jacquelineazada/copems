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
                  color="success"
                  variant="tonal"
                  class="status-chip"
                >
                  <v-icon start size="small">mdi-check-circle</v-icon>
                  Inspection Approved
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
                        <v-chip :class="getChipClass(item.status)" label size="small">
                          {{ item.status }}
                        </v-chip>
                      </td>
                      <td>{{ item.inspector }}</td>
                      <td>
                        <v-btn
                          color="#2563EB"
                          variant="text"
                          size="small"
                          @click="showApprovalDialog"
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
                    <span class="info-value font-weight-medium">10:30am</span>
                  </div>
                  <div class="summary-item mt-4">
                    <span class="info-label">Inspection Status</span>
                    <v-chip
                      size="small"
                      color="success"
                      variant="tonal"
                      class="status-chip"
                    >
                      Approved
                    </v-chip>
                  </div>
                </v-card-text>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
      </v-main>
    </v-layout>

    <v-dialog v-model="approvalDialog" max-width="500px">
      <v-card class="approved-dialog-card">
        <div class="approved-dialog-header d-flex align-center pa-4">
          <v-icon class="mr-2">mdi-check-circle</v-icon>
          <span class="text-h6 font-weight-bold">Inspection Approved</span>
          <v-spacer></v-spacer>
          <v-btn icon @click="approvalDialog = false" size="small" variant="text">
            <v-icon>mdi-close</v-icon>
          </v-btn>
        </div>
        <div class="pa-5">
          <v-card class="info-card" flat>
            <v-card-text>
              <v-row>
                <v-col cols="6" class="pb-0">
                  <div class="info-block">
                    <div class="info-label">Application Number</div>
                    <div class="info-value">BP-2024-000123-T</div>
                  </div>
                  <div class="info-block mb-0">
                    <div class="info-label">Approved By</div>
                    <div class="info-value">Chrize Tolosa</div>
                  </div>
                </v-col>
                <v-col cols="6" class="pb-0">
                  <div class="info-block">
                    <div class="info-label">Approval Date</div>
                    <div class="info-value">Jan 20, 2024</div>
                  </div>
                  <div class="info-block mb-0">
                    <div class="info-label">Application Type</div>
                    <div class="info-value">Full</div>
                  </div>
                </v-col>
              </v-row>
            </v-card-text>
          </v-card>
          <v-card class="fees-card mt-4" flat>
            <v-card-text>
              <div class="d-flex justify-space-between mb-2">
                <span class="fee-label">Assessment Fee</span>
              </div>
              <div class="d-flex justify-space-between">
                <span class="fee-label">Processing Fee</span>
              </div>
              <v-divider class="my-3"></v-divider>
              <div class="d-flex justify-space-between">
                <span class="fee-total">Total Amount</span>
              </div>
            </v-card-text>
          </v-card>
        </div>
        <v-card-actions class="pa-4 pt-2">
          <v-btn color="#16A34A" variant="flat" block size="large">
            <v-icon start>mdi-check-circle-outline</v-icon>
            Finalize Approval
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-card>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    // Data for breadcrumbs
    const breadcrumbs = ref([
      { title: "", disabled: false, href: "#" },
      { title: "", disabled: true },
    ]);

    // UPDATED: All inspection results are now "Passed"
    const inspectionResults = ref([
      { type: "Architectural Works", status: "Passed", inspector: "Eng. Joyce Oberos" },
      {
        type: "Civil/Structural Works",
        status: "Passed",
        inspector: "Eng. Roberto Martinez",
      },
      { type: "Electrical Works", status: "Passed", inspector: "Eng. Bernadette Veroza" },
      {
        type: "Sanitary Plumbing Works",
        status: "Passed",
        inspector: "Eng. Andrew Villapane",
      },
    ]);

    const approvalDialog = ref(false);

    const showApprovalDialog = () => {
      approvalDialog.value = true;
    };

    const getChipClass = (status) => {
      if (status === "Passed") {
        return "status-chip-passed";
      }
      return "status-chip-pending"; // Fallback
    };

    return {
      breadcrumbs,
      inspectionResults,
      getChipClass,
      approvalDialog,
      showApprovalDialog,
    };
  },
};
</script>

<style scoped>
/* ===================================== */
/* General Layout & Theme */
/* ===================================== */
.main-content {
  background-color: #f8f9fa;
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
.status-chip {
  font-weight: 500;
}
.status-chip-passed {
  font-weight: 500;
  border-radius: 16px;
  background-color: #dcfce7 !important;
  color: #16a34a;
}
.status-chip-pending {
  font-weight: 500;
  border-radius: 16px;
  background-color: #fef9c3 !important;
  color: #ca8a04;
}
/* ===================================== */
/* Inspection Schedule Side Card */
/* ===================================== */
.summary-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* ===================================== */
/* APPROVED DIALOG STYLES */
/* ===================================== */
.approved-dialog-card {
  border-radius: 12px !important;
}
.approved-dialog-header {
  background-color: #f0fdf4;
  color: #15803d;
}
.info-card {
  background-color: #ffffff;
  border: 1px solid #f3f4f6;
  border-radius: 12px;
}
.fees-card {
  background-color: #f8fafc !important;
  border: 1px solid #f3f4f6;
  border-radius: 12px;
}
.fee-label {
  font-size: 0.9rem;
  color: #667085;
}
.fee-total {
  font-size: 0.95rem;
  font-weight: 600;
  color: #101828;
}
</style>
