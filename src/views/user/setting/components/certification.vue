<template>
  <a-spin :loading="loading" style="width: 100%">
    <EnterpriseCertification :enterprise-info="data.enterpriseInfo" />
    <CertificationRecords :render-data="data.record" />
  </a-spin>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import {
  queryCertification,
  UnitCertification,
  EnterpriseCertificationModel
} from '@/api/user-center';
import useLoading from '@/hooks/useLoading';
import EnterpriseCertification from './enterprise-certification.vue';
import CertificationRecords from './certification-records.vue';

const { loading, setLoading } = useLoading(true);
const data = ref<UnitCertification>({
  enterpriseInfo: {} as EnterpriseCertificationModel,
  record: []
});
const fetchData = async () => {
  try {
    const resData = await queryCertification();
    data.value = resData;
  } catch {
    // todo
  } finally {
    setLoading(false);
  }
};
fetchData();
</script>

<style scoped lang="less"></style>
