<template>
  <v-card flat>
    <v-layout>
      <v-navigation-drawer v-model="drawer" :rail="rail" permanent @click="rail = false">
        <v-list>
          <v-list-item
            prepend-avatar="https://scontent.fwnp1-1.fna.fbcdn.net/v/t39.30808-6/482007057_953929396944205_496784858672308185_n.jpg?_nc_cat=102&ccb=1-7&_nc_sid=a5f93a&_nc_eui2=AeF3X7hm2ckriTf1-Bb5gNwhfMhmxxDF2Z18yGbHEMXZnS_SYFwo5FDnvG3qtrlx9DhRLvapomr0MD-fhRgSmoPW&_nc_ohc=v8O88NzBvuUQ7kNvwFnBIh7&_nc_oc=AdkMqwh_xy2CJbS7bdcvKQthrGkxfIU0vCgrH2ZVbbBnA6Np0dbxXdNN6IXhypXv0kI&_nc_zt=23&_nc_ht=scontent.fwnp1-1.fna&_nc_gid=pAhEG4OR1_QrK2dAYVpnug&oh=00_AfVz-qWewbXd1nBdAknpRHuxBCTdvevhQHYe3h1PGBRWg&oe=68A378B4"
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

      <v-main class="main-content">
        <v-toolbar color="transparent" flat>
          <v-toolbar-title class="toolbar-title"
            >Occupancy Permit Applicant Details</v-toolbar-title
          >
        </v-toolbar>

        <v-container fluid class="content-wrapper">
          <v-card class="header-card" flat>
            <v-card-text class="d-flex align-center">
              <v-avatar color="#3D71F2" size="56">
                <span class="text-h5 font-weight-bold">JM</span>
              </v-avatar>
              <div class="ml-4">
                <h1 class="header-title">Jm Deguzman</h1>
                <p class="header-subtitle">
                  jimdeguzman@gmail.com <br />
                  BP-2023-000-001
                </p>
              </div>
              <v-spacer></v-spacer>
              <v-chip size="default" color="#2563EB" variant="flat" class="status-chip">
                <v-icon start size="small">mdi-wrench-check-outline</v-icon>
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
                <v-card-title class="section-title">Inspection Results</v-card-title>
                <v-table class="inspection-table">
                  <thead>
                    <tr>
                      <th class="text-left text-subtitle-2">Inspection Type</th>
                      <th class="text-left text-subtitle-2">Status</th>
                      <th class="text-left text-subtitle-2">Inspector Name</th>
                      <th class="text-left text-subtitle-2">Actions</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="inspection in inspections" :key="inspection.type">
                      <td>{{ inspection.type }}</td>
                      <td>
                        <v-chip
                          :class="`status-chip-${inspection.status.toLowerCase()}`"
                          label
                          size="small"
                        >
                          {{ inspection.status }}
                        </v-chip>
                      </td>
                      <td>{{ inspection.inspectorName }}</td>
                      <td>
                        <v-btn variant="text" size="small" color="#2563EB"
                          >View Report</v-btn
                        >
                      </td>
                    </tr>
                  </tbody>
                </v-table>
              </v-card>
            </v-col>

            <v-col cols="12" lg="4">
              <v-card class="section-card inspection-schedule-card" flat>
                <v-card-title class="section-title">Inspection Schedule</v-card-title>
                <v-card-text>
                  <div class="d-flex justify-space-between align-center mb-4">
                    <span class="info-label">Date:</span>
                    <span class="info-value font-weight-medium">January 15, 2025</span>
                  </div>
                  <div class="d-flex justify-space-between align-center mb-4">
                    <span class="info-label">Time:</span>
                    <span class="info-value font-weight-medium">10:30am</span>
                  </div>
                  <div class="d-flex justify-space-between align-center">
                    <span class="info-label">Inspection Status:</span>
                    <v-chip size="default" color="warning" variant="tonal">
                      <v-icon start size="small">mdi-clock-outline</v-icon>
                      Pending Schedule
                    </v-chip>
                  </div>
                </v-card-text>
              </v-card>

              <v-card class="section-card" flat>
                <v-card-title class="section-title">Quick Actions</v-card-title>
                <v-card-text>
                  <v-btn block color="success" size="large" variant="flat">
                    <v-icon left>mdi-check-circle-outline</v-icon>
                    Approve Schedule
                  </v-btn>
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
    const drawer = ref(true);
    const rail = ref(true);

    const inspections = ref([
      {
        type: "Architectural Works",
        status: "Pending",
        inspectorName: "Eng. Joyce Oberos",
      },
      {
        type: "Civil/Structural Works",
        status: "Pending",
        inspectorName: "Eng. Roberto Martinez",
      },
      {
        type: "Electrical Works",
        status: "Pending",
        inspectorName: "Eng. Bernadette Venosoza",
      },
      {
        type: "Sanitary Plumbing Works",
        status: "Pending",
        inspectorName: "Eng. Andrew Villapane",
      },
    ]);

    return {
      drawer,
      rail,
      inspections,
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
.status-chip {
  font-weight: 500;
  color: #fff;
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
.inspection-schedule-card {
  background-color: #e3f2fd;
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
/* Inspection Table */
/* ===================================== */
.inspection-table {
  background-color: #ffffff;
  border-radius: 12px;
}

.inspection-table thead {
  background-color: #f5f5f5;
  border-bottom: 1px solid #e0e0e0;
}

.inspection-table th {
  font-weight: 600 !important;
  color: #4a4a4a !important;
  font-size: 0.8rem !important;
}

.inspection-table td {
  font-weight: 400 !important;
  color: #333333;
  font-size: 0.9rem;
}

.inspection-table tr:not(:last-child) td {
  border-bottom: 1px solid #e0e0e0;
}

/* Status Chips */
.status-chip-pending {
  background-color: #fef9c3;
  color: #c7ad00;
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
</style>
