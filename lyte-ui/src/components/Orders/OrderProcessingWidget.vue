<template>
    <div>
        <Doughnut :chart-data="chartData" :chart-options="chartOptions" />
    </div>
    
</template>

<script>

import { Doughnut } from 'vue-chartjs/legacy'
import { Chart as ChartJS, Title, Tooltip, Legend, CategoryScale, ArcElement } from 'chart.js'
ChartJS.register(Title, Tooltip, Legend, CategoryScale, ArcElement)

export default {
    name: 'OrderProcessingWidget',
    components: { Doughnut },
    data: () => ({
        chartData: {
            labels: [ 'Shipped', 'Picked', 'Allocated', 'Remaining'],
            datasets: [ { 
                data: [ 2, 10, 15, 30 ], // Shipped, Picked, Allocated, Orders
                cutout: '70%',
                circumference: 180,
                rotation: 270,
                backgroundColor: [
                    'rgba(75, 192, 192, 0.7)',
                    'rgba(255, 206, 86, 0.7)',
                    'rgba(255, 159, 64, 0.7)',
                    'rgba(255, 99, 132, 0.7)'
                ]
            } ]
        },
        chartOptions: {
            responsive: true,
            plugins: {
                legend: {
                    position: 'bottom'
                },
                title: {
                    display: true,
                    text: 'Weekly Orders Outstanding'
                }
            }
        }
    })
}
</script>