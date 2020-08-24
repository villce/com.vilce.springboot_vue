<template>
  <el-table class="wageOrder" :data="tableData" border style="width: 100%">
    <el-table-column fixed prop="order_time" label="日期" width="140" align='center'></el-table-column>
    <el-table-column prop="code" label="工号" width="80" align='center'></el-table-column>
    <el-table-column prop="name" label="姓名" width="80" align='center'></el-table-column>
    <el-table-column prop="basic_wage" label="基本工资" width="100" align='center'></el-table-column>
    <el-table-column prop="job_wage" label="岗位工资" width="100" align='center'></el-table-column>
    <el-table-column prop="benchmark_performance" label="基准绩效" width="100" align='center'></el-table-column>
    <el-table-column prop="standard_salary" label="标准工资" width="100" align='center'></el-table-column>
    <el-table-column prop="fixed_allowance" label="固定津贴" width="100" align='center'></el-table-column>
    <el-table-column prop="technical_expert_allowance" label="技术专家岗位津贴" width="140" align='center'></el-table-column>
    <el-table-column prop="rank_allowance" label="职级补贴" width="100" align='center'></el-table-column>
    <el-table-column prop="fixed_bonus" label="固定奖金" width="100" align='center'></el-table-column>
    <el-table-column prop="floating_bonus" label="浮动奖金" width="100" align='center'></el-table-column>
    <el-table-column prop="total_wages" label="工资共计" width="100" align='center'></el-table-column>
    <el-table-column prop="examination_allowance" label="考试津贴" width="100" align='center'></el-table-column>
    <el-table-column prop="on_off_after_leave_pay" label="入/离/事假后工资" width="140" align='center'></el-table-column>
    <el-table-column prop="performance_adjustment" label="绩效调整" width="100" align='center'></el-table-column>
    <el-table-column prop="floating_allowance" label="浮动津贴" width="100" align='center'></el-table-column>
    <el-table-column prop="daily_overtime" label="日常加班" width="100" align='center'></el-table-column>
    <el-table-column prop="sick_leave_deduction" label="病假扣除" width="100" align='center'></el-table-column>
    <el-table-column prop="late_absentee_deductions" label="迟到/旷工扣款" width="120" align='center'></el-table-column>
    <el-table-column prop="other_increase_or_decrease" label="其他增减" width="100" align='center'></el-table-column>
    <el-table-column prop="maternity_leave_deductions" label="产假扣款" width="100" align='center'></el-table-column>
    <el-table-column prop="floating_bonus2" label="浮动奖金2" width="100" align='center'></el-table-column>
    <el-table-column prop="recommendation_award" label="推荐奖" width="100" align='center'></el-table-column>
    <el-table-column prop="product_experience_bonus" label="产品体验/积分奖金" width="140" align='center'></el-table-column>
    <el-table-column prop="payable" label="应发工资" width="100" align='center'></el-table-column>
    <el-table-column prop="social_security" label="社保" width="80" align='center'></el-table-column>
    <el-table-column prop="provident_fund" label="公积金" width="100" align='center'></el-table-column>
    <el-table-column prop="post_insurance_pay" label="险金后工资" width="120" align='center'></el-table-column>
    <el-table-column prop="education_for_children" label="子女教育" width="100" align='center'></el-table-column>
    <el-table-column prop="home_loan" label="住房贷款" width="100" align='center'></el-table-column>
    <el-table-column prop="housing_rent" label="住房租金" width="100" align='center'></el-table-column>
    <el-table-column prop="support_for_the_elderly" label="赡养老人" width="100" align='center'></el-table-column>
    <el-table-column prop="continuing_education" label="继续教育" width="100" align='center'></el-table-column>
    <el-table-column prop="deferred_insurance" label="递延保险" width="100" align='center'></el-table-column>
    <el-table-column prop="tax" label="本月个税" width="100" align='center'></el-table-column>
    <el-table-column prop="paid_wages" label="实发工资" width="100" align='center'></el-table-column>
    <el-table-column fixed="right" label="操作" width="100" align='center'>
      <template slot-scope="scope">
        <el-button @click="handleClick(scope.row)" type="text" size="small">查看</el-button>
        <el-button @click="editWage()" type="text" size="small">编辑</el-button>
      </template>
    </el-table-column>
    <edit-form @onSubmit="getAllWageOrder()" ref="edit"></edit-form>
  </el-table>
</template>

<script>
import EditForm from './EditForm'
export default {
  name: 'WageOrder',
  components: EditForm,
  data () {
    return {
      tableData: []
    }
  },
  mounted: function () {
    this.getAllWageOrder()
  },
  methods: {
    getAllWageOrder () {
      var _this = this
      this.$axios.get('/wage/getAllWageOrder').then(resp => {
        if (resp && resp.status === 200) {
          if (resp.data.status === 0) {
            _this.tableData = resp.data.data
            console.info(_this.tableData)
          }
        }
      })
    },
    handleClick (row) {
      console.info(row)
      this.$refs.edit.dialogFormVisible = true
      this.$refs.edit.form = {
        eid: row.eid,
        code: row.code,
        name: row.name,
        order_time: row.order_time,
        basic_wage: row.basic_wage,
        job_wage: row.job_wage,
        benchmark_performance: row.benchmark_performance,
        standard_salary: row.standard_salary,
        fixed_allowance: row.fixed_allowance,
        technical_expert_allowance: row.technical_expert_allowance,
        rank_allowance: row.rank_allowance,
        fixed_bonus: row.fixed_bonus,
        floating_bonus: row.floating_bonus,
        total_wages: row.total_wages,
        examination_allowance: row.examination_allowance,
        on_off_after_leave_pay: row.on_off_after_leave_pay,
        performance_adjustment: row.performance_adjustment,
        floating_allowance: row.floating_allowance,
        daily_overtime: row.daily_overtime,
        sick_leave_deduction: row.sick_leave_deduction,
        late_absentee_deductions: row.late_absentee_deductions,
        other_increase_or_decrease: row.other_increase_or_decrease,
        maternity_leave_deductions: row.maternity_leave_deductions,
        floating_bonus2: row.floating_bonus2,
        recommendation_award: row.recommendation_award,
        product_experience_bonus: row.product_experience_bonus,
        payable: row.payable,
        social_security: row.social_security,
        provident_fund: row.provident_fund,
        post_insurance_pay: row.post_insurance_pay,
        education_for_children: row.education_for_children,
        home_loan: row.home_loan,
        housing_rent: row.housing_rent,
        support_for_the_elderly: row.support_for_the_elderly,
        continuing_education: row.continuing_education,
        deferred_insurance: row.deferred_insurance,
        tax: row.tax,
        paid_wages: row.paid_wages
      }
    }
  }
}
</script>
