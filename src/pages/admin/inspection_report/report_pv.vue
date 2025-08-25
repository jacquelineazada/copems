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
                          @click="showDetails(item)"
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

    <v-dialog v-model="dialog" max-width="800px">
      <v-card class="dialog-card" v-if="selectedInspection">
        <v-card-title class="dialog-title pa-4 d-flex align-center">
          <span class="text-h6 font-weight-bold"
            >{{ selectedInspection.type }} Report</span
          >
          <v-spacer></v-spacer>
          <v-btn icon @click="dialog = false" size="small" variant="text">
            <v-icon>mdi-close</v-icon>
          </v-btn>
        </v-card-title>
        <v-divider></v-divider>
        <v-card-text class="pa-6">
          <div class="d-flex justify-space-between align-start mb-6">
            <div>
              <div class="dialog-info-label">Assigned Inspector</div>
              <div class="dialog-info-value">{{ selectedInspection.inspector }}</div>
              <div class="dialog-info-label mt-3">Date of Inspection</div>
              <div class="dialog-info-value">
                {{ selectedInspection.details.inspectionDate }}
              </div>
            </div>
            <v-chip :class="getChipClass(selectedInspection.status)" class="mt-1" label>
              {{ selectedInspection.status }}
            </v-chip>
          </div>
          <div class="dialog-checklist">
            <div
              v-for="(item, i) in selectedInspection.details.checklist"
              :key="i"
              class="dialog-checklist-item"
            >
              <div class="dialog-checklist-title">{{ item.title }}</div>
              <p class="dialog-checklist-desc">{{ item.description }}</p>
            </div>
          </div>
        </v-card-text>
        <v-divider></v-divider>
        <v-card-actions class="pa-4">
          <v-btn variant="outlined" disabled>
            <v-icon left>mdi-chevron-left</v-icon>
            Previous
          </v-btn>
          <v-spacer></v-spacer>
          <span class="text-body-2 text-grey-darken-1">1 of 4</span>
          <v-spacer></v-spacer>
          <v-btn color="primary" variant="flat">
            Next
            <v-icon right>mdi-chevron-right</v-icon>
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <v-dialog v-model="violationDialog" max-width="600px">
      <v-card class="violation-dialog-card">
        <div class="violation-dialog-header d-flex align-center pa-4">
          <v-icon class="mr-2">mdi-message-alert-outline</v-icon>
          <span class="text-h6 font-weight-bold">Inspection with Violation</span>
          <v-spacer></v-spacer>
          <v-btn icon @click="violationDialog = false" size="small" variant="text">
            <v-icon>mdi-close</v-icon>
          </v-btn>
        </div>
        <div class="pa-5">
          <v-card class="violation-info-card" flat>
            <v-card-text>
              <v-row>
                <v-col cols="6">
                  <div class="info-block">
                    <div class="info-label">Application Number</div>
                    <div class="info-value">BP-2024-000123-T</div>
                  </div>
                  <div class="info-block mb-0">
                    <div class="info-label">Requested By</div>
                    <div class="info-value">Arch. Julian Lumanta</div>
                  </div>
                </v-col>
                <v-col cols="6">
                  <div class="info-block">
                    <div class="info-label">Request Date</div>
                    <div class="info-value">Jan 20, 2024</div>
                  </div>
                  <div class="info-block mb-0">
                    <div class="info-label">Status</div>
                    <v-chip class="status-chip-violation" label size="small">
                      <v-icon start size="x-small">mdi-clock-alert-outline</v-icon>
                      With Violation
                    </v-chip>
                  </div>
                </v-col>
              </v-row>
            </v-card-text>
          </v-card>
          <div class="mt-6">
            <div class="violation-section-title">With Deviation/Violation</div>
            <div v-for="v_type in violationTypes" :key="v_type" class="violation-item">
              {{ v_type }}
            </div>
          </div>
          <div class="mt-6">
            <div class="violation-section-title mb-2">Detailed Remarks</div>
            <v-textarea
              v-model="detailedRemarks"
              label="Enter remarks"
              variant="outlined"
              rows="4"
              counter="500"
              maxlength="500"
              no-resize
            ></v-textarea>
          </div>
        </div>
        <v-divider></v-divider>
        <v-card-actions class="pa-4">
          <v-spacer></v-spacer>
          <v-btn variant="outlined" class="px-6" @click="violationDialog = false"
            >Cancel</v-btn
          >
          <v-btn color="#3366FF" variant="flat" class="px-6">
            <v-icon start>mdi-send</v-icon>
            Send Request
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-card>
</template>

<script>
import { ref, computed } from "vue";

export default {
  setup() {
    // Data for breadcrumbs
    const breadcrumbs = ref([
      { title: "", disabled: false, href: "#" },
      { title: "", disabled: true },
    ]);

    // Data for the inspection results table
    const inspectionResults = ref([
      {
        type: "Architectural Works",
        status: "Passed",
        inspector: "Eng. Joyce Oberos",
        details: {
          inspectionDate: "06/07/2023",
          checklist: [
            {
              title: "Application for Building Permit",
              description:
                "The necessary application for the building permit has been completed.",
            },
            {
              title: "Scaffolding & Sidewalk",
              description:
                "Preparations and assessments related to scaffolding and sidewalk requirements have been addressed.",
            },
            {
              title: "Safety Requirements for Construction/Demolition",
              description:
                "All essential safety requirements for construction and/or demolition activities have been met.",
            },
          ],
        },
      },
      {
        type: "Civil/Structural Works",
        status: "Passed",
        inspector: "Eng. Roberto Martinez",
        details: {
          inspectionDate: "06/07/2023",
          checklist: [
            {
              title: "Application for Building Permit",
              description:
                "The necessary application for the building permit has been completed.",
            },
            {
              title: "Structural Hazards",
              description:
                "Identified structural hazards have been assessed and addressed.",
            },
            {
              title: "Others",
              description:
                "Additional miscellaneous items or considerations have been reviewed.",
            },
          ],
        },
      },
      {
        type: "Electrical Works",
        status: "Violation",
        inspector: "Eng. Bernadette Veroza",
      },
      {
        type: "Sanitary Plumbing Works",
        status: "Violation",
        inspector: "Eng. Andrew Villapane",
      },
    ]);

    const dialog = ref(false);
    const violationDialog = ref(false); // New dialog state
    const selectedInspection = ref(null);
    const detailedRemarks = ref(""); // State for the textarea

    // Computed property to get all violation types
    const violationTypes = computed(() => {
      return inspectionResults.value
        .filter((item) => item.status === "Violation")
        .map((item) => item.type);
    });

    const showDetails = (item) => {
      selectedInspection.value = item;
      if (item.status === "Passed" && item.details) {
        dialog.value = true;
      } else if (item.status === "Violation") {
        detailedRemarks.value = ""; // Reset remarks
        violationDialog.value = true;
      }
    };

    const getChipClass = (status) => {
      switch (status) {
        case "Passed":
          return "status-chip-passed";
        case "Violation":
          return "status-chip-violation";
        default:
          return "status-chip-pending";
      }
    };

    return {
      breadcrumbs,
      inspectionResults,
      getChipClass,
      dialog,
      violationDialog,
      selectedInspection,
      detailedRemarks,
      violationTypes,
      showDetails,
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
.status-chip-pending,
.status-chip-passed,
.status-chip-violation {
  font-weight: 500;
  border-radius: 16px;
}
.status-chip-pending {
  background-color: #fef9c3 !important;
  color: #ca8a04;
}
.status-chip-passed {
  background-color: #dcfce7 !important;
  color: #16a34a;
}
.status-chip-violation {
  background-color: #fee2e2 !important;
  color: #ef4444;
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
/* ===================================== */
/* PASSED DIALOG STYLES */
/* ===================================== */
.dialog-card {
  border-radius: 12px !important;
}
.dialog-title {
  color: #101828;
}
.dialog-info-label {
  color: #667085;
  font-size: 0.8rem;
}
.dialog-info-value {
  color: #101828;
  font-weight: 500;
  font-size: 0.9rem;
}
.dialog-checklist-item {
  margin-bottom: 1.5rem;
}
.dialog-checklist-item:last-child {
  margin-bottom: 0;
}
.dialog-checklist-title {
  font-size: 1rem;
  font-weight: 600;
  color: #101828;
  margin-bottom: 4px;
}
.dialog-checklist-desc {
  font-size: 0.9rem;
  color: #475467;
  line-height: 1.5;
}

/* ===================================== */
/* VIOLATION DIALOG STYLES */
/* ===================================== */
.violation-dialog-card {
  border-radius: 12px !important;
}
.violation-dialog-header {
  background-color: #fff1f2;
  color: #dc2626;
}
.violation-info-card {
  background-color: #ffffff;
  border: 1px solid #f3f4f6;
  border-radius: 12px;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05);
}
.violation-section-title {
  color: #475467;
  font-weight: 600;
  font-size: 0.9rem;
  margin-bottom: 0.5rem;
}
.violation-item {
  color: #101828;
  font-weight: 500;
  font-size: 0.95rem;
  margin-bottom: 0.5rem;
}
</style>
