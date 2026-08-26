using System;

namespace Infosys.EmployeeManagement
{
    public class Employee
    {
        private static int employeeId = 1000;

        public string EmployeeId { get; set; }
        public string EmployeeName { get; set; }
        public int UnitId { get; set; }
        public string ProjectCode { get; set; }
        public double Salary { get; set; }
        public int JobLevel { get; set; }
        public DateTime JoiningDate { get; set; }

        public Employee()
        {
            employeeId++;
            EmployeeId = "E" + employeeId;
        }
    }
}
