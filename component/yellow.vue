<template>
	<div class="yellow-box">
	  <div class="yellow-box-header">
		<span class="yellow-label">Yellow:</span>
	  </div>
	  <span class="yellow-content">
		<slot></slot>
	  </span>
	</div>
  </template>

  <style>
  .yellow-box {
	background-color: #fef3c7; /* Soft yellow - Tailwind's bg-yellow-100 */
	padding: 0.5rem;
	border-radius: 0.5rem;
	display: flex;
	flex-direction: column;
	margin: 0.5rem 0;
  }

  .yellow-box-header {
	display: flex;
	align-items: center;
  }

  .yellow-label {
	/*background-color: #fcd34d; /* Brighter yellow - roughly Tailwind's bg-yellow-300 */
	color: #f59e0b; /* text-yellow-500 */
	font-weight: 600;
	font-size: 1rem;
	margin-left: 0.375rem;
	padding: 0.2rem 0.4rem;
	border-radius: 0.25rem;
  }

  .yellow-content {
	background-color: rgba(255, 255, 255, 0.5);
	padding: 0.5rem;
	margin-top: 0.25rem;
	border-radius: 0.375rem;
	color: #a16207; /* text-yellow-700 */
  }
  </style>
