<template>
  <v-app style="background-color: #f8f9fa">
    <v-main class="d-flex align-center justify-center">
      <v-container>
        <v-row justify="center">
          <v-col cols="12" md="10" lg="8">
            <v-card class="checklist-card" flat>
              <v-card-title class="text-h5 font-weight-bold pa-6">
                Electrical Works Checklist
              </v-card-title>
              <v-divider></v-divider>
              <v-card-text class="pa-6">
                <div
                  v-for="item in checklistItems"
                  :key="item.id"
                  class="checklist-item-row"
                >
                  <v-checkbox
                    v-model="item.checked"
                    hide-details
                    class="flex-shrink-0 mr-4"
                  ></v-checkbox>
                  <div class="item-label">{{ item.label }}</div>
                  <v-text-field
                    v-model="item.remarks"
                    density="compact"
                    variant="outlined"
                    label="Enter remarks..."
                    hide-details
                    class="remarks-field"
                  ></v-text-field>
                </div>

                <div class="mt-6">
                  <v-checkbox
                    v-model="others.checked"
                    hide-details
                    label="Others"
                    color="primary"
                  ></v-checkbox>
                  <v-textarea
                    v-model="others.details"
                    class="mt-4"
                    variant="outlined"
                    label="Enter detailed structural assessment findings..."
                    rows="4"
                    no-resize
                  ></v-textarea>
                </div>
              </v-card-text>
              <v-divider></v-divider>
              <v-card-actions class="pa-4">
                <v-spacer></v-spacer>
                <v-btn
                  color="success"
                  variant="flat"
                  size="large"
                  @click="openConfirmDialog('PASSED')"
                >
                  <v-icon left>mdi-check</v-icon>
                  Passed
                </v-btn>
                <v-btn
                  color="error"
                  variant="flat"
                  size="large"
                  class="ml-2"
                  @click="openConfirmDialog('VIOLATION')"
                >
                  <v-icon left>mdi-close</v-icon>
                  Violation
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>

    <v-dialog v-model="confirmDialog" max-width="400px" persistent>
      <v-card rounded="lg">
        <v-card-title class="text-h6 font-weight-bold"> Confirm Action </v-card-title>
        <v-card-text>
          Are you sure you want to mark this inspection as {{ confirmActionType }}?
        </v-card-text>
        <v-card-actions class="pa-4">
          <v-spacer></v-spacer>
          <v-btn variant="outlined" @click="confirmDialog = false">Cancel</v-btn>
          <v-btn color="success" variant="flat" @click="handleConfirm">Confirm</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <v-dialog v-model="reportDialog" max-width="800px">
      <v-card class="report-dialog-card">
        <v-card-title class="d-flex align-center">
          <span class="text-h6 font-weight-bold">Electrical Works Report</span>
          <v-spacer></v-spacer>
          <v-btn icon @click="reportDialog = false" variant="text" size="small">
            <v-icon>mdi-close</v-icon>
          </v-btn>
        </v-card-title>
        <v-card-text>
          <div class="d-flex justify-space-between align-start mb-6">
            <div>
              <div class="report-info-label">Assigned Inspector</div>
              <div class="report-info-value">Eng. Joyce Oberos</div>
              <div class="report-info-label mt-3">Date of Inspection</div>
              <div class="report-info-value">06/07/2025</div>
            </div>
            <v-chip
              v-if="confirmActionType === 'PASSED'"
              color="success"
              variant="tonal"
              label
              >Passed</v-chip
            >
            <v-chip
              v-if="confirmActionType === 'VIOLATION'"
              color="error"
              variant="tonal"
              label
              >Violation</v-chip
            >
          </div>

          <div class="report-checklist">
            <div v-if="confirmActionType === 'PASSED'">
              <div
                v-for="item in passedItems"
                :key="item.id"
                class="report-checklist-item"
              >
                <div class="report-checklist-title">{{ item.label }}</div>
                <p class="report-checklist-desc">{{ item.description }}</p>
              </div>
              <div v-if="others.checked" class="report-checklist-item">
                <div class="report-checklist-title">Others</div>
                <p class="report-checklist-desc">
                  Additional miscellaneous items or considerations have been reviewed.
                </p>
              </div>
            </div>
            <div v-if="confirmActionType === 'VIOLATION'">
              <div class="report-checklist-title mb-2">Items with Violations:</div>
              <div
                v-for="item in violationItems"
                :key="item.id"
                class="report-checklist-item"
              >
                <div class="report-checklist-title violation">{{ item.label }}</div>
              </div>
            </div>
          </div>
        </v-card-text>
        <v-card-actions class="pa-4">
          <v-spacer></v-spacer>
          <v-btn color="primary" variant="flat" size="large">
            <v-icon left>mdi-send</v-icon>
            Submit Report
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-app>
</template>

<script>
import { ref, computed } from "vue";

export default {
  setup() {
    // UPDATED: Checklist is now complete
    const checklistItems = ref([
      {
        id: 1,
        label: "General Requirements",
        description: "All general electrical requirements have been met.",
        checked: false,
        remarks: "",
      },
      {
        id: 2,
        label: "General Wiring Method",
        description:
          "Preparations and assessments related to wiring have been addressed.",
        checked: false,
        remarks: "",
      },
      {
        id: 3,
        label: "Services, Feeders & Branch Circuits",
        description:
          "The necessary application for the building permit has been completed.",
        checked: false,
        remarks: "",
      },
      {
        id: 4,
        label: "Grounding & Bonding",
        description: "All essential safety requirements have been met.",
        checked: false,
        remarks: "",
      },
      {
        id: 5,
        label: "Hazardous Locations",
        description: "Identified structural hazards have been assessed and addressed.",
        checked: false,
        remarks: "",
      },
      {
        id: 6,
        label: "Special Occupanciess",
        description: "Requirements for special occupancies have been reviewed and met.",
        checked: false,
        remarks: "",
      },
      {
        id: 7,
        label: "Swimming Pools & Related Installations",
        description:
          "Electrical systems for pools and related installations are compliant.",
        checked: false,
        remarks: "",
      },
      {
        id: 8,
        label: "Emergency & Standby Systems & Fire Pumps",
        description: "Emergency systems and fire pumps are correctly installed.",
        checked: false,
        remarks: "",
      },
    ]);

    const others = ref({
      checked: true,
      details: "",
    });

    const confirmDialog = ref(false);
    const reportDialog = ref(false);
    const confirmActionType = ref("");

    const passedItems = computed(() => {
      return checklistItems.value.filter((item) => item.checked);
    });

    const violationItems = computed(() => {
      return checklistItems.value.filter((item) => !item.checked);
    });

    const openConfirmDialog = (actionType) => {
      confirmActionType.value = actionType;
      confirmDialog.value = true;
    };

    // UPDATED: Now handles both PASSED and VIOLATION
    const handleConfirm = () => {
      confirmDialog.value = false;
      if (
        confirmActionType.value === "PASSED" ||
        confirmActionType.value === "VIOLATION"
      ) {
        reportDialog.value = true;
      }
    };

    return {
      checklistItems,
      others,
      confirmDialog,
      reportDialog,
      confirmActionType,
      passedItems,
      violationItems,
      openConfirmDialog,
      handleConfirm,
    };
  },
};
</script>

<style scoped>
.checklist-card {
  border: 1px solid #e0e0e0;
  border-radius: 12px;
}
.checklist-item-row {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
  gap: 16px;
}
.item-label {
  flex: 1;
  font-weight: 500;
  color: #000000ff;
}
.remarks-field {
  max-width: 350px;
}
.v-btn {
  text-transform: none;
  font-weight: 600;
}

/* Report Dialog Styles */
.report-dialog-card {
  border-radius: 12px !important;
}
.report-info-label {
  color: #667085;
  font-size: 0.8rem;
}
.report-info-value {
  color: #101828;
  font-weight: 500;
  font-size: 0.9rem;
}
.report-checklist-item {
  margin-bottom: 1.5rem;
}
.report-checklist-item:last-child {
  margin-bottom: 0;
}
.report-checklist-title {
  font-size: 1rem;
  font-weight: 600;
  color: #101828;
  margin-bottom: 4px;
}
.report-checklist-title.violation {
  color: #d32f2f; /* Red color for violation titles */
}
.report-checklist-desc {
  font-size: 0.9rem;
  color: #475467;
  line-height: 1.5;
}
</style>
