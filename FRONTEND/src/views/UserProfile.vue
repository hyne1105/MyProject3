
<script>
import { mapState } from "pinia";
import { useAuthStore } from "@/stores/Auth.store";
import HeaderShop from "../components/HeaderShop.vue";
import FooterShop from '@/components/FooterShop.vue';
import EditUser from "../components/EditUser.vue";
import toastsVue from "../components/toasts.vue";
export default {
	data() {
		return {
			checkedit: false,
		}
	},
	components: {
		HeaderShop,
		EditUser,
		toastsVue,
		FooterShop,
	},
	computed: {
		...mapState(useAuthStore, {
			currentUser: "user",
		}),
	},
	methods: {
		showedit() {
			if (!this.checkedit) {
				this.checkedit = true;
			}
			else {
				this.checkedit = false;
			}
		},

	}
};
</script>
<template>
	<HeaderShop></HeaderShop>
	<toastsVue></toastsVue>
	<div class="d-flex justify-content-center">
		<div class="container profile shadow-sm p-3 mb-5 bg-body rounded">
			<header>
				<h4 class="py-4 text-center text-muted">THÔNG TIN KHÁCH HÀNG </h4>
			</header>
			<div class="container">
				<div class="row" v-if="currentUser">
					<div class="pr1 d-flex justify-content-center">
						<div class="row" style="width: 400px;">
							<div class="col-9">
								<p>
									<strong class="text-muted">Tên tài khoản:</strong>
									{{ currentUser.username }}
								</p>
								<p>
									<strong class="text-muted">Email:</strong>
									{{ currentUser.email }}
								</p>
							</div>
							<div class="col-3 pt-2">
								<button class="Btn" @click="showedit"><div style="font-size: 10px;">Chỉnh sửa</div>
									<svg class="svg" viewBox="0 0 512 512">
										<path
											d="M410.3 231l11.3-11.3-33.9-33.9-62.1-62.1L291.7 89.8l-11.3 11.3-22.6 22.6L58.6 322.9c-10.4 10.4-18 23.3-22.2 37.4L1 480.7c-2.5 8.4-.2 17.5 6.1 23.7s15.3 8.5 23.7 6.1l120.3-35.4c14.1-4.2 27-11.8 37.4-22.2L387.7 253.7 410.3 231zM160 399.4l-9.1 22.7c-4 3.1-8.5 5.4-13.3 6.9L59.4 452l23-78.1c1.4-4.9 3.8-9.4 6.9-13.3l22.7-9.1v32c0 8.8 7.2 16 16 16h32zM362.7 18.7L348.3 33.2 325.7 55.8 314.3 67.1l33.9 33.9 62.1 62.1 33.9 33.9 11.3-11.3 22.6-22.6 14.5-14.5c25-25 25-65.5 0-90.5L453.3 18.7c-25-25-65.5-25-90.5 0zm-47.4 168l-144 144c-6.2 6.2-16.4 6.2-22.6 0s-6.2-16.4 0-22.6l144-144c6.2-6.2 16.4-6.2 22.6 0s6.2 16.4 0 22.6z">
										</path>
									</svg>
								</button>
							</div>

						</div>

					</div>

				</div>
				<div class="row py-5 d-flex justify-content-center" v-if="checkedit">
					<EditUser :user="currentUser"></EditUser>
				</div>


			</div>

		</div>
	</div>
	<FooterShop></FooterShop>
</template>

<style>
.profile {
	background-color: white;
	margin: 30px;
	min-height: 400px;
	max-width: 600px;
}

.pr1 {
	margin: auto;
}
</style>
