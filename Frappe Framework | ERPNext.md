# Frappe Framework and ERPNext Installation and Usage Notes

## Install Frappe Bench and ERPNext version 13 (stable):

    bench init --frappe-branch version-13 frappe-bench
    cd ~/frappe-bench
    bench get-app erpnext https://github.com/frappe/erpnext --branch version-13

Check:

    bench version

## Usage:

    bench new-site sitename                         # add new site
    bench --site sitename install-app erpnext       # install erpnext app at site 
    
    
